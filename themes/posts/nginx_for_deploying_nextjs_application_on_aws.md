+++
category = "technical"
title = "NGINX for Deploying Next.js Application on AWS EC2 with AWS ELB — Control and Stability of Deployments"
date = 2024-01-29
+++

*I was looking for an article like this a few days ago, which I didn’t find at that time, so I did the deployment on my own and came up with this article to prevent other developers from saving those efforts and focusing on development. I am not explaining every single step and have provided links for references.*

I prefer manual deployment of applications over automated (and even serverless) methods. Although they are convenient and require less effort by the developers, they are bound to the providers and offer less control over the underlying system. It’s an absolute necessity that the systems work as the developer (or a team in the organisation) wants it to, and not more than that. Often, more in this situation means more pricing which is considered for a long period can sum up to a huge amount, and even that functionality may not be that good enough or even required.

A simple deployment that ensures the control of the developing team and offers no more than the requirements is an efficient way to deploy applications. Consolidating these advantages, simplicity in design opens more doors to innovation and developing unique solutions to occurring problems. I believe that innovation requires freedom and control over a certain thing that is meant to be improved. Automated tools which act like an invisible layer of internal mechanisms for deployment often don’t allow the deployment team to work on their terms and end up causing a steep learning curve and fewer own-built features.

Next Js is widely used for developing web applications due to its vast ecosystem and convenience. Although there are a lot of ways to deploy these applications to a certain extent, having manually operated servers provides a degree of freedom and access to the resources. AWS (Amazon Web Services) provides lots of ways of deployment (like AWS Amplify but they are automated, or Virtual Machines for Manual Control). AWS EC2 (Elastic Compute Cloud) provides manual control over the servers with a whole degree of freedom to manage and extend the usage. Coupled with EC2, AWS ELB (Elastic Load Balancer) provides a convenient way to balance multiple EC2 Instances and prevent failures due to large amounts of requests, by distributing loads over lots of machines. NGINX provides proxy handling for configuring the right ports in the server.

![diagram](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*DkzBa69AD0Y4BD-uMB2N3g.png)

The combination of Next Js, NGINX, AWS EC2 and AWS ELB provides a system with high throughput, control and upgradability to the organisation, ensuring efficient pricing and usage of the system. Configuring them can be tricky in some cases, but here is a suckless guide to walk through the process.

## Get an AWS EC2 Instance Running

On the AWS portal, get the EC2 instance and deploy it. For Next Js, my personal preference goes with using Linux, especially Debian (although Ubuntu Servers are good too and are based on Debian). Choose enough capacity EC2 Instance and connect to it via SSH.

Refer to AWS EC2 Docs: https://docs.aws.amazon.com/ec2/

## Build the Next Js Application
Once the application is ready for deployment, start building the project. It’s not a big deal for deployment engineers whether to use npm or yarn, but use anything that works out best for you. As this is a production environment, you would need to build it and then run it on the EC2 Instance.

```bash 
npm install 
npm run build 
npm install -g pm2
pm2 start npm --name "your-application-name" -- start
pm2 save
pm2 startup
```

This will fire up pm2 (process manager for node.js) which will run on the server in the background. The startup command would make sure that the Next Js application gets up when the server reboots. This ensures uptime in cases of the server rebooting (although the load balancer will manage it but it’s good if the server revokes itself).

Now the application must be running on port 3000 (default port). To route the traffic to port 80 (HTTP port), you need to proxy requests using NGINX. NGINX routes the traffic from one port to another and vice-versa.

## Setting up NGINX for Proxy

NGINX is easy to configure and requires a single configuration file to get the work done. First, install NGINX into the server. For Debian-based servers:

```bash 
sudo apt update
sudo apt install nginx
```

Create a config file `your-application-name.conf` in the `/etc/nginx/conf.d/` directory. Here is a basic and minimal config template that you can use, which works just fine:

```bash 
server {
    listen 80; # Listen on port 80

    server_name <domain-name or IP address>;

    location / {
        proxy_pass http://127.0.0.1:3000; # Proxy traffic to port 3000
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

Yes, you can use IP addresses too in the **server_name** field in case you don’t have a domain name yet. It’s the part where I spend most of my time debugging, it’s a field where you need to add what the user enters in the search bar when accessing the application.

At last, start NGINX with the following commands (for Debian-based servers):

```bash 
systemctl enable nginx
systemctl start nginx
```

This will start nginx and configure it to start when the system reboots too.

## Set Up Elastic Load Balancer

Configuring AWS ELB can be done on the AWS console and the docs can be referred for purposes. You just need to route traffic from ELB port 80 to EC2 port 80. The options in the ELB are absolutely easy and can be done with fet Google searches on the way. ELB has options to add more instances in case you have more instances running the application.

A point to note here is that you can skip the process of using NGINX and set up the ELB to forward traffic to EC2 port 3000 (default port of Next Js).

Refer to AWS ELB docs: https://docs.aws.amazon.com/elasticloadbalancing/

## Conclusion
This was a simple guide to setting up a deployment which is scalable, manual and provides a greater degree of control than automated deployment tools. This can be integrated with a lot of external tools like GitHub actions to create a CI/CD Pipeline.

This guide was something that I needed a few days ago and now it exists.

