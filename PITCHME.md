---

<span style="font-weight: bold; font-size: 170%; color:#FFFF00">FOSS: Docker Containers</span>

June 7, 2019
#### Tyson Lee Swetnam Ph.D.
<img src="assets/imagery/cyverse_white.png" width="500">


+++

## Why Containerize?

- Dependencies turn into wicked problems <!-- .element: class="fragment" -->
- Compiling software is sloooowww <!-- .element: class="fragment" -->
- Reproducibility is hard across platforms <!-- .element: class="fragment" -->
- Portability <!-- .element: class="fragment" --> **& _Scalability_** <!-- .element: class="fragment" -->

+++

## Install data science software on CyVerse Atmosphere

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/4/4e/Docker_%28container_engine%29_logo.svg/2000px-Docker_%28container_engine%29_logo.svg.png" height="150"><img src="https://www.sylabs.io/wp-content/uploads/2018/10/s-icon.png" height="150"><img src="http://jupyter.org/assets/hublogo.svg" height="150">

+++

@title[EZ Install]

## <span style="color: #e49436">EZ Install</span>
<br>

```shell
$ ezd -p
$ sudo usermod -aG docker $USER
$ exit
```

@[1](install Docker and Portainer.io)
@[2](change `sudo` privileges)
@[3](exit and restart terminal window)

+++

## Choose your own adventure:

- <span style="font-weight: bold; font-size: 80%; color:#55FF33">Newbie: Find a container that already exists on https://hub.docker.com/</span>
- <span style="font-weight: bold; font-size: 80%; color:#F9FF33">Veteran: Modify an existing container recipe, adding new dependencies</span> 
- <span style="font-weight: bold; font-size: 80%; color:#FF0000">Elite: Create your own recipe from scratch</span>

+++

## Find a container that already exists on a Docker Registry 

+++
<img src="assets/imagery/Rlogonew.png" height="150"> <img src="https://www.rstudio.com/wp-content/uploads/2014/07/RStudio-Logo-Blue-Gradient.png" height="150">

```shell
$ docker pull rocker/geospatial:latest
$ docker images
$ docker run --rm -d -p 8787:8787 -e PASSWORD=password rocker/geospatial:latest
$ docker ps
$ docker stop <container id>
Done!

```

@[1](pull the latest version of Rocker Geospatial RStudio-Server from DockerHub)
@[2](List stored container images in your Docker cache)
@[3](Run the Container in detached mode `-d` on port `-p 8787:8787`)
@[4](List running container instances)
@[5](Runs RStudio-Server in the background, open it in a new browser tab)

+++

# Build your own Docker Container from scratch

+++
## <span style="color: #e49436">Create a Dockerfile</span>
<br>

```shell
FROM ubuntu:18.04
MAINTAINER "Tyson Lee Swetnam" tswetnam@cyverse.org
RUN apt-get update && apt-get install -y fortune cowsay lolcat
ENV PATH=/usr/games:${PATH}
ENV LC_ALL=C
ENTRYPOINT fortune | cowsay | lolcat

```

@[1](FROM a image base, e.g. alpine, centos, debian, ubuntu, I use Ubuntu Bionic Beaver 18.04)
@[2](Add in who the person was who created the container - not required)
@[3](RUN a set of scripts, here an update and installation of three programs)
@[4](Set the environment, adding the three new games to the PATH)
@[5](Use the default language)
@[6](the ENTRYPOINT is what will happen when the container is run)

+++

@title[DOCKER]

## <span style="color: #e49436">Build your Docker container</span>
<br>


```shell
$ sudo docker build -t tswetnam/cowsay:latest .
$ docker run -it tswetnam/cowsay:latest 
$ docker run --rm -it --entrypoint /bin/bash tswetnam/cowsay:latest 
$ fortune | cowsay | lolcat
$ docker push tswetnam/cowsay:latest

Done!
```

@[1](Use `sudo` to build the image with a tag name)
@[2](Run new image using the interactive and TTY flags)
@[3](Start a bash shell inside the container - note: you're inside the container now)
@[4](Run the programs from inside the container)
@[5](Push your container to DockerHub)
@[7](Done!)

---?image=assets/imagery/endslide.png


