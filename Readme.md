<h1 align="center">
  <br>
  <a href="https://www.youracclaim.com/org/ibm/badge/docker-essentials-a-developer-introduction"><img src="https://acclaim-production-app.s3.amazonaws.com/images/08216781-93cb-4ba1-8110-8eb3401fa8ce/Docker%2BEssentials%2B-%2BISDN.png" alt="Markdownify" width="200"></a>
  <br>
  
  <br>
</h1>

<h1 align="center">Docker Essentials: A Developer Introduction
</p>


# Get Started
Objectives
When you finish this course, you should understand:

* What containers are and their benefits
* How to find and run Docker containers from the Docker Hub
* How to create your first Docker container and understand the layering and union file system
* The best practices when developing Dockerfiles
* How to solve problems of orchestration: reconciliation, scaling, high availability, and service discovery
* Some of the tools that can help you run highly available applications in production, such as the IBM Container service

# Lab 1: Run your first container 
[Youtube - Lab 1 Overview](https://www.youtube.com/watch?time_continue=161&v=Mycr9j-jgYo)

## WHAT ARE CONTAINERS? 

* A group of processes run in isolation
    - All processes MUST be able to run on the shared kernel

* Each container has its own set of "namespaces"(isolated view)
    - PID: process IDs
    - USER: user and group IDs
    - UTS: hostname and domain name
    - NS mount points
    - NET: Network devices, stacks, ports
    - IPC: inter-process communications, message queues

* cgroups - controls limits and monitoring of resources

### VM vs Container
![](./images/vm_vs_container.png)

### What is Docker
* At its core, Docker is tooling to manage containers
    - Simplified existing technology to enable it for the masses
* Enable developers to use containers for their applications
    - Package dependencies with containers: "build once, run anywhere"

### Why Continers are Appealing to Users
* No more "Works on my machine"
* Lightweight and fast
* Better resource utilization
    - Can fit far more containers that VMs into a host
* Standard developer to operations interface
* Ecosystem and tooling

## Lab overview
* Containers are just a process (or a group of processes) running in isolation, which is achieved with Linux namespaces and control groups. Linux namespaces and control groups are features that are built into the Linux kernel. Other than the Linux kernel itself, there is nothing special about containers.

* What makes containers useful is the tooling that surrounds them. The labs in this course use Docker, which has been the understood standard tool for using containers to build applications. Docker provides developers and operators with a friendly interface to build, ship, and run containers on any environment.

* In the first part of this lab, run your first container, and learn how to inspect it. You will be able to witness the namespace isolation that you acquire from the Linux kernel.

* After you run your first container, you can explore other uses of docker containers. You can find many examples of these on the Docker Store and can run several different types of containers on the same host, which allows you to see the benefit of isolation—where you can run multiple containers on the same host without conflicts.

## Run a container
> 1. Open a terminal on your local computer and run this command: `docker container run -t ubuntu top`

You use the docker container run command to run a container with the Ubuntu image by using the top command. The -t flag allocates a pseudo-TTY, which you need for the top command to work correctly.

The docker run command first starts a docker pull to download the Ubuntu image onto your host. After it is downloaded, it will start the container. The output for the running container should look like this:

1. Install Docker
    - OS: MaC
    ```bash
    brew cask install docker

2. Running docker
![](./images/running_docker.png)


3. run this command:
    ```bash
    docker container run -t ubuntu top

> The `docker run` command first starts a docker pull to download the Ubuntu image onto your host. After it is downloaded, it will start the container. The output for the running container should look like this:

![](./images/running_ubuntu.png)


* `top` is a Linux utility that prints the processes on a system and orders them by resource consumption. Notice that there is only a single process in this output: it is the `top` process itself. You don't see other processes from the host in this list because of the PID namespace isolation.

* Containers use Linux namespaces to provide isolation of system resources from other containers or the host. The PID namespace provides isolation for process IDs. If you run `top` while inside the container, you will notice that it shows the processes within the PID namespace of the container, which is much different than what you can see if you `ran` top on the host.

* Even though we are using the Ubuntu image, `it is important to note that the container does not have its own kernel`. It uses the kernel of the host and the Ubuntu image is used only to provide the file system and tools available on an Ubuntu system.

2. Inspect the container:
```
docker container exec
```
This command allows you to enter a running container's namespaces with a new process.



3. Open a new terminal. To open a new terminal connected to node1 by using Play-With-Docker.com, click `Add New Instance` on the left and then ssh from node2 into node1 by using the IP that is listed by node1, for example:

4. In the new terminal, get the ID of the running container that you just created:

```
docker container ls 
 ```
5. Use that container ID to run bash inside that container by using the docker container exec command. Because you are using bash and want to interact with this container from your terminal, use the -it flag to run using interactive mode while allocating a psuedo-terminal:

```
 docker container exec -it b3ad2a23fab3 bash 
root@b3ad2a23fab3:/#
```

6. From the same terminal, inspect the running processes:

```
ps -ef
```

![](https://courses.cognitiveclass.ai/asset-v1:IBMDeveloperSkillsNetwork+CO0101EN+v1+type@asset+block/lab1_step1_3b.png)

7. For comparison, exit the container and run ps -ef or top on the host. These commands will work on Linux or Mac. For Windows, you can inspect the running processes by using tasklist.

```
root@b3ad2a23fab3:/# exit 
exit
$ ps -ef
# Lots of processes!
```


<!-- * LivePreview - Make changes, See changes
  - Instantly see what your Markdown documents look like in HTML as you create them.
* Sync Scrolling
  - While you type, LivePreview will automatically scroll to the current location you're editing.
* GitHub Flavored Markdown  
* Syntax highlighting
* [KaTeX](https://khan.github.io/KaTeX/) Support
* Dark/Light mode
* Toolbar for basic Markdown formatting
* Supports multiple cursors
* Save the Markdown preview as PDF
* Emoji support in preview :tada:
* App will keep alive in tray for quick usage
* Full screen mode
  - Write distraction free.
* Cross platform
  - Windows, macOS and Linux ready. -->

<!-- ## How To Use

To clone and run this application, you'll need [Git](https://git-scm.com) and [Node.js](https://nodejs.org/en/download/) (which comes with [npm](http://npmjs.com)) installed on your computer. From your command line:

```bash
# Clone this repository
$ git clone https://github.com/amitmerchant1990/electron-markdownify

# Go into the repository
$ cd electron-markdownify

# Install dependencies
$ npm install

# Run the app
$ npm start
```

Note: If you're using Linux Bash for Windows, [see this guide](https://www.howtogeek.com/261575/how-to-run-graphical-linux-desktop-applications-from-windows-10s-bash-shell/) or use `node` from the command prompt.


## Download

You can [download](https://github.com/amitmerchant1990/electron-markdownify/releases/tag/v1.2.0) the latest installable version of Markdownify for Windows, macOS and Linux.

## Credits

This software uses the following open source packages:

- [Electron](http://electron.atom.io/)
- [Node.js](https://nodejs.org/)
- [Marked - a markdown parser](https://github.com/chjj/marked)
- [showdown](http://showdownjs.github.io/showdown/)
- [CodeMirror](http://codemirror.net/)
- Emojis are taken from [here](https://github.com/arvida/emoji-cheat-sheet.com)
- [highlight.js](https://highlightjs.org/)

## Related

[markdownify-web](https://github.com/amitmerchant1990/markdownify-web) - Web version of Markdownify

## Support

<a href="https://www.buymeacoffee.com/5Zn8Xh3l9" target="_blank"><img src="https://www.buymeacoffee.com/assets/img/custom_images/purple_img.png" alt="Buy Me A Coffee" style="height: 41px !important;width: 174px !important;box-shadow: 0px 3px 2px 0px rgba(190, 190, 190, 0.5) !important;-webkit-box-shadow: 0px 3px 2px 0px rgba(190, 190, 190, 0.5) !important;" ></a>

<p>Or</p> 

<a href="https://www.patreon.com/amitmerchant">
	<img src="https://c5.patreon.com/external/logo/become_a_patron_button@2x.png" width="160">
</a>

## You may also like...

- [Pomolectron](https://github.com/amitmerchant1990/pomolectron) - A pomodoro app
- [Correo](https://github.com/amitmerchant1990/correo) - A menubar/taskbar Gmail App for Windows and macOS -->

## License

<!-- MIT

---

> [amitmerchant.com](https://www.amitmerchant.com) &nbsp;&middot;&nbsp;
> GitHub [@amitmerchant1990](https://github.com/amitmerchant1990) &nbsp;&middot;&nbsp;
> Twitter [@amit_merchant](https://twitter.com/amit_merchant) -->
