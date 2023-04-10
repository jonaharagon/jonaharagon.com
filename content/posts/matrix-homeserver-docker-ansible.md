---
title: Create Your Matrix Homeserver with Docker and Ansible
date: 2021-07-31
---
Matrix is a modern, open standard for decentralized communications. It boasts a production-ready specification maintained by [the Matrix.org Foundation](https://matrix.org/) and it’s being used by anyone from small hobbyist collectives to national governments. Essentially, it’s an instant messaging service, but one that can be under your complete control: Your data won’t be snooped through by Big Tech organizations, and it won’t stop existing because one company decides they want to shut it down.

At the heart of Matrix are “homeservers”, individual servers running some software that connects to the Matrix network via federation. You may have heard of and use another federated platform: Email. Much like how email allows users of gmail.com, hotmail.com, or your-own-domain.com to all email each other, you can use Matrix by signing up for a big service like [matrix.org](https://element.io/get-started), or run one yourself. You can message anyone on Matrix regardless of which homeserver your user and your data is hosted on.

## What You'll Need

All you’ll need to get started is a server running Debian 9 or newer, Ubuntu 16.04 or newer, Arch Linux, or CentOS 7 (CentOS 8 has some  [unresolved issues](https://github.com/spantaleev/matrix-docker-ansible-deploy/issues/300)  with this script at the time of writing). For single-user instances Synapse is fairly lightweight, and you can run it for as little as $5/month from any major VPS provider.

You’ll also need a  domain name which you are able to change the DNS records for. You’ll want to create two  `A`  records (subdomains):  `matrix`  and  `element`, both pointing to your VPS’s IP address.

## Getting the Playbook

You can follow these steps on your own computer or on the server itself. We’re going to download a set of open-source scripts (the  _Playbook_) from GitHub that will automatically install  **Synapse**  (the reference Matrix homeserver software) on your VPS. Using Git, download the script repo from GitHub:

```bash
git clone [https://github.com/spantaleev/matrix-docker-ansible-deploy.git](https://github.com/spantaleev/matrix-docker-ansible-deploy.git)
```

This is going to create a folder called  `matrix-docker-ansible-deploy`  , and the rest of these commands are going to be run from within this folder, so you can switch to it now:

```bash
cd matrix-docker-ansible-deploy
```

## Configuring the Playbook

First you’ll want to create a folder to hold your server’s configuration we’ll be setting up in a second. Replace  `<your-domain>`  in these commands with your own domain name, of course:

```bash
mkdir inventory/host_vars/matrix.<your-domain>
```

Next, we’ll want to copy the sample configuration to that new folder:

```bash
cp examples/vars.yml inventory/host_vars/matrix.<your-domain>/vars.yml
```

We’ve created a  `vars.yml`  file in the folder you created which has some basic configuration already included. Open up that file in your favorite text editor to configure your server, it really only takes a few simple changes.

![](https://miro.medium.com/v2/resize:fit:1400/1*bEQlB87Lka5KSptqfqkbBg@2x.png)

-   `matrix_domain`  should be your domain name,  **without**  the  `matrix` subdomain. This domain is going to be a part of your username, which will look like  `@jane:example.com`. You wouldn’t want to include the  `matrix`  subdomain here for the same reason it’d look a bit silly if your email was  `jane@email.example.com`.
-   `matrix_ssl_lets_encrypt_support_email`  should point to any email address of yours. You probably won’t receive any emails, this is only needed to obtain an SSL certificate for your homeserver, but in case that process fails you’ll get a notification at this address.
-   `matrix_coturn_turn_static_auth_secret`,  `matrix_synapse_macaroon_secret_key`, and  `matrix_postgres_connection_password`  should all be set to long, random strings.

You can use  `pwgen`  to generate those long, random strings. They won’t need to be memorable at all, so let’s generate some random data:

```bash
pwgen -s 64 1
```

Run it three times to generate different strings for all of them, just to be safe.

Once you’ve filled out the configuration file, we’re going to create one more file to tell Ansible what your server’s IP address actually is, and then we’ll be set!

Create the file  `inventory/hosts`  and edit it with your favorite text editor. In it, you should add the following:

```
[matrix_servers]  
matrix.<your_domain> ansible_host=<your_VPS_EXTERNAL_IP> ansible_ssh_user=root
```

If you’re setting up all this configuration on the server you’re actually installing this on rather than your own computer, add  `ansible_connection=local`  to the end of that last line as well.

## Installing Synapse

We’ve finished all the configuration we need! To get the installation started, we’ll need Ansible installed on the computer we made these configuration files on. You can  [install Ansible via most package managers](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#installing-ansible-on-specific-operating-systems)  or  [manually](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#). For example, on macOS you can install Ansible with:

```bash
brew install ansible
```

Then inside that  `matrix-docker-ansible-deploy`  folder, all you need to run is:

```bash
ansible-playbook -i inventory/hosts setup.yml --tags=setup-all
```

This command gets everything installed and ready to go on your server! The fantastic thing about Ansible is that any time you think something’s  _off_  with your server, you can just re-run this command and it will check your installation and fix anything that doesn’t match the configuration we’re installing now.

Once it finishes up, everything should be installed! Not everything will be started yet however, one more run will actually turn everything on and make sure everything starts automatically after a reboot:

```bash
ansible-playbook -i inventory/hosts setup.yml --tags=start
```

And that’s it! For federation to work however, there is one final step.

## Enabling Federation

We’ve created a homeserver at  **_matrix_**_.your-domain.com_, but you want your username to just have  _your-domain.com_  at the end. To do this, we need to serve two delegation files on your main domain via HTTP. There are two ways to do this:

1.  Point your main domain name to the Matrix server we just created, or
2.  Create these files on your existing webserver.

### Option 1: Dedicating your entire domain to Matrix

If you aren’t going to use your domain name for a website or anything other than Matrix, this is the simplest option: Just point your root domain name to the Matrix homeserver as well, and have the webserver we created with Ansible serve the delegation files.

First, edit your DNS configuration and add an  `A`  record to your base domain pointing to the IP address of your Matrix server.

Next, we’ll make one simple modification to the  configuration files we created earlier. Edit  `inventory/host_vars/matrix.<your_domain>/vars.yml`  and add the following line to the end of the file:

```
matrix_nginx_proxy_base_domain_serving_enabled: true
```

Then, re-run this command to add this new configuration to your homeserver:

```bash
ansible-playbook -i inventory/hosts setup.yml --tags=setup-all,start
```

### Option 2: Add two files to your existing webserver

Maybe you’re already using your domain name for something else, like a website or blog. You’ll just have to create two files on whatever server hosts your existing site.

`/.well-known/matrix/server`:

```
{  
	"m.server": "matrix.<your_domain>:8448"  
}
```

and  `/.well-known/matrix/client`:

```
{  
	"m.homeserver": {  
		"base_url": "https://matrix.<your_domain>"  
	},  
	"m.identity_server": {  
		"base_url": "https://matrix.<your_domain>"  
	},  
	"io.element.e2ee": {  
		"default": true,  
		"secure_backup_required": false,  
		"secure_backup_setup_methods": []  
	},  
	"im.vector.riot.e2ee": {  
		"default": true  
	}  
}
```

## Creating a User

The last step in this getting started guide is creating your user account. You can run the following command to create a user, just fill in everything between  `<>`s:

```
ansible-playbook -i inventory/hosts setup.yml --extra-vars='username=<your-username> password=<your-password> admin=<yes|no>' --tags=register-user
```

Alternatively, you can connect to your homeserver via SSH and run:

```bash
/usr/local/bin/matrix-synapse-register-user <your-username> <your-password>
```

There’s lots of  [configuration changes](https://github.com/spantaleev/matrix-docker-ansible-deploy/blob/master/docs/registering-users.md)  that will let you do things like share a registration page with other people, or launch an Admin Web GUI for managing your server, but this should get us started as a single-user instance for now.

## And that’s it!

Once you have Matrix installed and the delegation files setup so that other homeservers can federate with yours, you should be all set!

The  `[matrix-docker-ansible-deploy](https://github.com/spantaleev/matrix-docker-ansible-deploy)`  project on GitHub has  [an extensive collection of documentation](https://github.com/spantaleev/matrix-docker-ansible-deploy/tree/master/docs)  if you’re looking for additional features, or for  [upgrading](https://github.com/spantaleev/matrix-docker-ansible-deploy/blob/master/docs/maintenance-upgrading-services.md)  your services as new versions are released.

If installing and maintaining a Matrix homeserver is a bit over your head, but you still want to take control of your instant messaging platform,  [NABLA HOST](https://nablahost.net/)  has a range of affordable  [Synapse homeserver hosting options starting at $10/month](https://my.nablahost.net/index.php?rp=/store/matrix-hosting), as well as Matrix installation and maintenance services where we get everything set up on the server of your choice, you could even run a homeserver from your own home! We specialize in services for individuals and small businesses, but we can work with groups of any size to help find the right Matrix solution for your needs.
