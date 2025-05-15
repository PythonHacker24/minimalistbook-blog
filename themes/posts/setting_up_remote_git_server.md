+++
category = "technical"
title = "Setting Up a Remote Git Server — A Simple and Concise Step-by-Step Guide to Host a Private Git Server"
date = 2024-02-10
+++

*Preface: This is a concise and simple guide to hosting a remote git server. I have been researching this topic for a while and came up with the idea of writing an article with a step-by-step guide for hosting a private git server. Covering all the aspects of git is not possible in a single article, so it’s assumed that the reader has prior knowledge of git and version control.*

## Introduction to Private Remote Git Server

A private remote git server allows multiple developers to collaborate and develop software with the comfort of version control. All the codebase and files would be stored in the remote git repository with each change tracked systematically. Although there are plenty of options to go with for remote git management services, owning a private server provides the organisation with more control over their data as well as customisations they can make over their property. These git servers can be paired with domain names for convenience and hence, the organisation enjoys the ownership of its data.

If the software is intended to be hosted openly for the public, a simple web interface works fine here and would be covered here (having a domain name like `git.domain-name.tld` can be done here).

To set up a remote git server, you need the resources mentioned here:

1. Remote Linux Server (I prefer Debian and Cloud-based) as per the requirements and load-handling capabilities
2. Computer to SSH into the Server
3. Domain Name (Optional)

The size of the Linux Server is as per the requirements of the organisation. This depends upon the load to withstand, the size of the files, network load, availability, etc. I usually prefer cloud servers for easy processes and upgradability if required (vertical scaling).

## Setting Up a “git” User in the Remote Git Server

The first step is to SSH into your remote server (or even have a physical connection and access it, doesn’t matter) and log into it.

The service that is going to run on the remote git server would be running as the “git” user. Although any user can use it and even root works fine, but this would cause a security issue and hence is not recommended. Also using a username called “git” would work systematically in future settings.

To add a new user on Debian:

```bash 
sudo adduser git
su git
```
This will ask a couple of questions that can be resolved and the terminal will now log in as the “git” user. Now all the configurations (unless stated) would be done with this user. It’s a good idea to configure only git-related configurations with the user for security purposes.

## Setting Up SSH Access to the Remote Git Server

This is the part where access to all the participants of the Git Server would be provided. This can be updated in future too to add more participants to the git server. This required generating their SSH private and public key with the following commands and adding them to the remote server.

On the participant's computer (if id_rsa file exists on the computer, this part can be skipped):

```bash 
cd ~/
cd .ssh 
ssh-keygen
```
In case the `.ssh` directory is not found, create it by `mkdir .ssh` command. The `ssh-keygen` command generated a private and public key. While naming them, it's a good practice to name them `id_rsa` which would allow the `ssh` command to work without `-i` to provide a key, it would self-detect the file. At the end of this procedure, two files will be generated: `id_rsa` and `id_rsa.pub` and will be stored in the `.ssh` directory.

This needs to be done on all the participant’s computers to create access keys to the remote git server.

Now the Public Keys generated need to be provided to the remote git server. It can be done via the following commands (in the “git” user):

```bash 
kdir .ssh
chmod 700 .ssh/
touch .ssh/authorized_keys
chmod 600 .ssh/authorized_keys
vim .ssh/authorized_keys
```

Any text editor can be used here instead of Vim. In this file, all the Public Keys need to be appended. On the participant’s computer, `cat .ssh/id_rsa.pub` and copy-paste it into the `.ssh.authorized_keys` file on the remote git server. All the public keys must be pasted one by one on each line.

After this procedure, all the participants whose public keys were appended would be able to SSH into the git server without any password (due to the public key being present in the `.ssh` directory).

## Setting Up Required Tools in the Remote Git Server

The server now requires to installation of the tools given below with the commands (Here, Debian commands would be provided. Although this must work with almost all Linux systems and only tools are required. It can be done with any package manager).

```bash 
sudo apt update && sudo apt upgrade
sudo apt install git gitweb fcgiwrap nginx
```
This will install the required tools for setting up the remote git server. For reference, `git` is the version control application. `gitweb` would provide a web interface for the git server. `fcgiwrap` is a simple FastCGI wrapper for CGI scripts required for `Nginx` and nginx is the HTTP server for the web application to run.

## Setting Up the Repository in the Remote Git Server

This step requires switching to the `root` user. A git directory needs to be created where all the projects would be stored. The official git server documentation uses `/srv/git` which can be used or even it’s as per the server administrator to store the projects. Although, it is recommended to do it in `/var/www/git`. This is because this folder is intended to be the hosting section of Linux Server. The `/var/www/html` is where the apache2 service hosts the files from. So it’s convenient to have the `git` there. Again, it can be done anywhere on the server.

```bash 
mkdir /var/www
mkdir /var/www/git
chown git:git git/
cd git
su git
```
The `chown` command transferred the ownership of the file to the “git” user. Now all the projects would be stored in this directory. For demonstration purposes, a directory called `dotfiles.git` can be created. This directory is usually used to have a backup of scripts that are required to run a computer that was developed by the user (note the “.git” extension at the end of the directory name).

```bash 
mkdir dotfiles.git
```
Now to initiate this project:

```bash 
git init --bare
```
Now the git server has been configured with a project called `dotfiles.git` and can be used to store projects and get files stored into it. Multiple projects can be created as per the requirements and the procedure remains the same.

## Configuring Local Repositories to Remote Git Server

The Local Repositories on the participant’s computers now need to be configured with the Remote Git Server. This requires editing a file in the `.git` folder in the repository.

```bash
vim .git/config
```
Again, any text editor can be used instead of Vim. Now a remote section needs to be added to the config file.

```bash 
[remote "<name>"]
  url = <username>@<server-ip or domain-name>:<absolute-path-to-project>.git
  fetch = +refs/heads/*:refs/remotes/home/*
```

For example, if all instructions all followed including references, it might look like this:

```bash 
[remote "git-server"]
  url = git@<server-ip or domain-name>:/var/www/git/dotfiles.git
  fetch = +refs/heads/*:refs/remotes/home/*
```

Now git is ready to push the contents from the local repository to the remote git repository. This can be done with the commands:

```bash 
git push <name> <branch-name>
```

For example with previous references, it might look like this:

```bash 
git push git-server master
```
Done! now all the content from the local git repository would be pushed into the remote git repository.

This can be verified in the remote git server by going to the project file and using the command `git log` which would contain the logs of commit and pushes done.

## Setting Up Web Interface for the Remote Git Server

To set up the Web Interface for your Remote Git Server, you need to expose port 80 (for HTTP) or port 443 (for HTTPS). Here, steps for an HTTP server are provided as HTTPS configuration is out of the scope of this article. Hence, port 80 must be open and it should be made sure that the firewall is not blocking incoming or outgoing traffic on port 80 (usually, cloud servers have this by default closed and need to be configured manually).

Here, gitweb would be used to create the website files and content management. Furthermore, Nginx would be used to host these files. To set gitweb, the following commands can be used:

```bash 
sudo vim /etc/gitweb.conf
```

Again, any text editor would do the job. Here, the `$projectroot` needs to be modified. It should be set to the directory of projects. Regarding the previous steps, it should look like this:

```bash 
$projectroot = "/var/www/git"
```

If in any part modifications of files throw any issue, try using `sudo` to get superuser rights to do it.

After this, the Nginx needs to be configured. To do this, a file needs to be created in the `/etc/nginx/sites-available` directory. The following commands can be used:

```bash 
sudo touch /etc/nginx/sites-available/<file-name>.conf
sudo vim /etc/nginx/sites-available/<file-name>.conf
```

The “file-name” can be anything. To configure this file, the following configuration can be used:

```bash 
server {
  listen 80;
  server_name <domain-name or server-ip>;

  location /index.cgi {
    root /usr/share/gitweb/;
    include fastcgi_params;
    gzip off;
    fastcgi_param SCRIPT_NAME $uri;
    fastcgi_param GITWEB_CONFIG /etc/gitweb.conf;
    fastcgi_pass  unix:/var/run/fcgiwrap.socket;
  }

  location / {
    root /usr/share/gitweb/;
    index index.cgi;
  }

}
```

The “server_name” variable needs to be configured as per the domain name or the IP address (in case there is no domain name configured with the IP address).

To start the Nginx Server, the following commands can be used:

```bash 
sudo systemctl restart nginx
```

Done! The web interface will be available now on the domain name or IP address.

At this point, a full-fledged Remote Git Server has been set up on the remote server and can be used for the development and distribution of code.

## Conclusion

Owning a private remote git server allows developers to have total control over their data and allows them to manage it as per their requirements. During the process of setting it up, there might be issues even if the guide is thoroughly followed, as it always happens. This can be resolved with some troubleshooting on the internet or by going through the official documents of the tools used in this process. Although efforts have been made to make this guide self-sufficient to walk-through developers to set up a remote git repository, issues persist in varying environments.

The link to official docs is provided here:

Git Docs: https://git-scm.com/doc

Git Remote Server Docs:https://git-scm.com/book/en/v2/Git-on-the-Server-Setting-Up-the-Server

Nginx Docs: https://docs.nginx.com/

fcgiwrap Docs:
- https://github.com/gnosek/fcgiwrap
- https://www.nginx.com/resources/wiki/start/topics/examples/fcgiwrap/

