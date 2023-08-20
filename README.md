#### This project is for the Devops bootcamp exercise for

#### "Cloud Basics"


Demo Project:
	Create server and deploy application on DigitalOcean

Technologies used:
	DigitalOcean, Linux, Java, Gradle

Project Description 
	Setup and configure a server on DigitalOcean
	Create and configure a new Linux user on the Droplet
	(Security best practice)
	Deploy and run a Java Gradle application on Droplet


Use repository: https://gitlab.com/twn-devops-bootcamp/latest/05-cloud/cloud-basics-exercises

You are asked to create a simple NodeJS app that lists all the projects each developer is working on. Everyone on your team wants to be able to see the list themselves and share with the project managers, so they ask you to make it available online, so everyone can access it.


EXERCISE 0: Clone Git Repository

For that you can use my provided git repository.

 [x] clone the git repository and
 [x] create your ownproject/git repo from it
	https://github.com/EvgeniyKunegin/cloud-basics-exercises

EXERCISE 1: Package NodeJS App

To have just 1 file, you create an artifact from the Node App. So you do the following:

- [x]  Package your Node app into a tar file (npm pack)

	\cloud-basics-exercises\app>npm pack


EXERCISE 2: Create a new server

Your company uses DigitalOcean as Infrastructure as a Service platform, instead of having on-premise servers. So you:
- [x] Create a new droplet server on DigitalOcean
  https://cloud.digitalocean.com/droplets/369795809    

EXERCISE 3: Prepare server to run Node App

Now you have a new fresh server nothing installed on it. Because you want to run a NodeJS application you need to install Node and npm on it:

- [x] Install nodejs & npm on it
	evgen@ubuntu-s-1vcpu-512mb-10gb-fra1-01:~$ node -v
	v12.22.9
	
	evgen@ubuntu-s-1vcpu-512mb-10gb-fra1-01:~$ npm -v
	8.5.1
      

EXERCISE 4: Copy App and package.json

Having everything prepared for the application, you finally:

- [x] Copy your simple Nodejs app tar file and package.json to the droplet

	scp ./app/bootcamp-node-project-1.0.0.tgz evgen@165.232.75.42:/home/evgen/app-list
	scp .\app\package.json evgen@165.232.75.42:/home/evgen/app-list

	:~$ ls app-list | grep boot*
	bootcamp-node-project-1.0.0.tgz


EXERCISE 5: Run Node App

- [x] Start the node application in detached mode (npm installand node server.jscommands)

	Extracting
	tar -xvf bootcamp-node-project-1.0.0.tgz

npm install 
node server.js &


EXERCISE 6: Access from browser - configure firewall
You see that the application is not accessible through the browser, because all ports are closed on the server. So you:

- [x] Open the correct port on Droplet
- [x] and access the UI from browser

	$ sudo netstat -lpnt
	Active Internet connections (only servers)
	tcp6       0      0 :::3000                 :::*                    LISTEN      7277/node
	
	:~/app-list$ ps aux | grep "node server.js"
	evgen       7277  0.0  3.7 624700 17404 ?        Sl   Aug19   0:00 node server.js