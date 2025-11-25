# Deploy-an-App-with-Docker
Docker is a platform that lets you package applications and all their dependencies into containers, which run the same on any system.

# Deploy an App with Docker


**Author:** Darryl Brown  
**Email:** darrylbrown1991@gmail.com

---

![Image](http://learn.nextwork.org/sincere_vermilion_playful_beaver/uploads/aws-compute-eb_c4df13c84)

---

## Introducing Today's Project!

### What is Docker?

Docker is a platform that lets you package applications and all their dependencies into containers, which run the same on any system. Containers are lightweight, fast to start, and isolated, making them ideal for development, testing, and production. Docker ensures consistency across environments, the “it works on my machine” problems disappear, simplifies deployment, and helps teams scale applications efficiently. It's widely used in DevOps, microservices, CI/CD pipelines, and cloud environments because it improves reliability, portability, and automation.

### One thing I didn't expect...

One thing I didn't expect in this project was for Elastic Beanstalk to create and use other AWS resources similarly to CloudFormation.

### This project took me...

This project took me approximately 45 minutes. The most rewarding part was just putting Docker and AWS Elastic Beanstalk together.

---

## Understanding Containers and Docker

### Containers

Containers are tools for and everything it needs to run in one file. Now other developers can run this package instead of the application itself, which gets the application working much faster. They are useful because it help developers/engineers working in a team together to share their work in a more efficient way. 

A container image is a blueprint or template for making containers. It tells Docker exactly what to put inside each container, things like your app’s code, the libraries it needs, and any other required files.

### Docker

Docker helps create, manage, and deploy these containers efficiently. You can think of Docker as a tool that helps create the cargo and load them onto ships. Docker Desktop is a program that makes it easy to work with Docker, a tool for creating and managing containers. Engineers use Docker Desktop to build, test, and deploy applications right from their computers.

The Docker daemon is the engine, in more technical terms, the Docker daemon is a background process that manages the Docker containers on your computer. It takes commands from the Docker client or terminal and does the heavy lifting of building, running, and distributing your containers.

---

## Running an Nginx Image

Nginx is a web server, which is a program used to run websites and web apps. If you want people to visit your site, you're going to need a web server to deliver your website's files to their browsers. Engineers sometimes pick Nginx when they need to manage lots of visitors at once, making sure the site doesn’t slow down when traffic spikes. Nginx is also the web server of choice in some cases for containerized apps because it's lighter and uses less memory, compared to other options like Apache.

The command I ran to start a new container was 
"docker run -d -p 80:80 nginx" . "docker run" starts a new container. I'm using an existing container image called "nginx" and I'm starting this container in detached mode (-d) so it runs in the background. Then, this -p 80:80 maps port 80 on my host machine to port 80 in the container, which means I'll be able to access the webpage that Nginx is running through my computer's web browser.


![Image](http://learn.nextwork.org/sincere_vermilion_playful_beaver/uploads/aws-compute-eb_6245f5bb10)

---

## Creating a Custom Image

The Dockerfile is a document with all the instructions for building my Docker image. Docker would read a Dockerfile to understand how to set up my application's environment and which software packages it should install.

My Dockerfile tells Docker three things:
1.) "FROM nginx:latest", means my image starts as a copy of the latest Nginx image, but I'll make a few modifications/additions to it to customize it for what I need.
2.) "COPY index.html /usr/share/nginx/html/" replaces the default HTML file provided by Nginx with my own custom index.html file, so I'm customizing the Nginx server to serve my own web content.
3.) "EXPOSE 80" means I want the container to receive web traffic through port 80, which makes it easier for users and other services to reach my web app. 

The command I used to build a custom image with my Dockerfile was "docker build -t my-web-app . "
The " . " (period)  at the end of the command tells Docker to find the Dockerfile in the current directory, which would be the Compute folder I created locally.

![Image](http://learn.nextwork.org/sincere_vermilion_playful_beaver/uploads/aws-compute-eb_4c741d1913)

---

## Running My Custom Image

There was an error when I ran my custom image because when there's already a container using port 80 the new container I created can't access it. I resolved this by running this command showing me the container ID using port 80 "docker ps --filter "publish=80". Then ran this command to stop that container freeing up port 80 for my new created container image " docker stop <CONTAINER-ID> "

In this example, the container image is the blueprint that tells Docker the application code, dependencies, libraries that should go into a container.  The container is the actual software that's created from this image and running the web server displaying my index.html.

![Image](http://learn.nextwork.org/sincere_vermilion_playful_beaver/uploads/aws-compute-eb_74b5c3d619)

---

## Elastic Beanstalk

Elastic Beanstalk is a service that makes it easy to deploy cloud applications without worrying about the underlying infrastructure. I simply upload my code and Elastic Beanstalk handles everything needed to get it running, like setting up servers and managing scaling. This lets me focus on my application code without having to spend too much time on managing cloud infrastructure.

Deploying my custom image with Elastic Beanstalk didn't take long.

![Image](http://learn.nextwork.org/sincere_vermilion_playful_beaver/uploads/aws-compute-eb_26d5573b23)

---

## Deploying App Updates

To learn how to deploy app updates with Elastic Beanstalk, I updated my app by adding more lines to my index.html file. I verified those changes by opening the .html file in my firefox browser.

My app updates didn't show up in my live environment immediately because I had to upload and deploy updated application files. To deploy my changes, I only had to upload update application files and let AWS Elastic Beanstalk do the rest.

![Image](http://learn.nextwork.org/sincere_vermilion_playful_beaver/uploads/aws-compute-eb_5b7034684)

---

---
