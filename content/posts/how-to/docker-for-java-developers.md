---
title: "Docker for Java Developers"
date: 2019-05-03T11:09:41+00:00
draft: false
Difficulty: Beginner
---

**Pre-requisites**

- Operating System: Windows
- GitHub account
- JDK
- Eclipse

This quick tutorial helps you install Docker on a Windows machine and get the application running on a Web browser. The application is a Java application and a self-paced, hands-on way to understand Docker.
For the code repo, please see 

```
`https://github.com/docker/labs/tree/master/developer-tools/java/`
```

## What is Docker?

Docker is an open platform for developing, shipping, and running applications. The applications are packaged and run in a format called a container. For a more detailed read, the [Docker](https://docs.docker.com/engine/docker-overview/) documentation is a great resource.

## Set the environment

1. Install Docker
For the tutorial, I have installed Docker Toolbox on a Windows machine.
If you have an old Windows machine like me, then you can
get the installation from [here](https://docs.docker.com/toolbox/overview/).

But it is **advisable** to switch to the latest versions of Windows. The Toolbox includes the docker-machine and docker-compose commands. Once you are done installing Docker, test your Docker installation by running the following command. Use a bash or terminal to run the above command.

```
`docker run hello-world`
```

If you don't have the image in your repo, Docker will automatically pull the image from the Docker Hub and you should get a message that your installation is working fine.

2. Download the Java IDE of your choice. I have installed Eclipse.
Install [Eclipse IDE](https://www.eclipse.org/downloads/packages/) for Java EE Developers.

3. [Latest Java Development Kit](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)

4. [Maven for Eclipse](https://www.eclipse.org/m2e/)

## Getting started

1. On the command line, clone the repo [registration-docker](https://github.com/docker/labs)

```
`git clone https://github.com/docker/labs`
```

```
`cd labs/developer-tools/java-debugging`
```

2. The project should be exported as a Maven project on Eclipse. Build the application and after the Maven build, you should get a **Build Success** message.

![](/images/docker-for-java-developers/eclipse_wrkspace.png)

3. Running the application

- Open the Docker Quick Start Terminal. The Toolbox will show a valid IP address once Docker is started.- Navigate to the application path where the yml file is located.- `Run docker-compose up`- Docker will build the image for Tomcat and a MySQL database and start the container. The project is loaded in the Tomcat webapps directory in the web server container.

4. Open the browser and type `localhost:8080` and you should be able to see the Tomcat home page. This indicates that the web server is ready!
If you are not able to load using localhost, use the IP of your machine.

![](/images/docker-for-java-developers/tomcat.png)

5. To go to the application, Click on `/UserSignup` link.

# ![](/images/docker-for-java-developers/usersignup.png)

Click on the Signup button to create a new user.

![](/images/docker-for-java-developers/signup.png)

**Congrats**! This completes a quick deployment of a Java web application on Docker. For troubleshooting, explore the GitHub [link](https://github.com/docker/labs/blob/master/developer-tools/java/chapters/appb-troubleshooting.adoc).
