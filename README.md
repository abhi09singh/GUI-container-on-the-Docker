#GUI container on the Docker : [running jupyter notebook on Docker container for ML model training]#

https://www.linkedin.com/pulse/task02-gui-container-docker-running-jupyter-notebook-ml-abhinav-singh/?trackingId=U002vHA5mlpfRviUsv0VZw%3D%3D

Above task is divided into following sub-task:

🔰Launch a container on docker in GUI mode 

🔰Run any GUI software on the container

Pre-requisites:
Host OS should be GUI
Docker installed in your OS
Host OS should be GUI as Host OS will share the DISPLAY with the Docker container, and the container will assume it has a display.

STEP-1 : Launch a container on docker in GUI mode

Firstly we will create a workspace in our host os.
No alt text provided for this image
🌐 Now it's time to create our own Docker Image. There are two methods of doing this — Docker Commit Command & Dockerfile concept. I want to talk about Dockerfile.

Remember one thing that our final goal is not just to launch the OS. Our final goal is to run our programs inside container. So, for that either we can launch one container & can run our program, but in Industry we run thousands of containers in parallel.
This is the reason we want to create Docker Image & for that purpose we use “Dockerfile” concept. On your Docker Host create one folder to use as your workspace & then inside that workspace create one file using vim or gedit editor. One small thing to note here is that the file name should be “Dockerfile” only. 
No alt text provided for this image
No alt text provided for this image
Save the file & now let's understand how this file has been written. Dockerfile has it's own specific keywords to tell certain things. Like we used “FROM” keyword to tell use “centos:latest” image & on top of this image we will run our program.
Next to run any program we need to install the required software, for that we used “RUN” keyword & tell to use “yum install <required packages>” command to install the software. Just note one thing that as we are using “centos:latest” to run our program that's why to install the software we used “yum” command.
most important point to note here is we need some extra packages dependencies like "Packagekit-gtk3-module" and " libcanberra-gtk2 module" to run gui application in docker container. During my research i found out that firefox when made to run over centOS or RHEL ,it kept looking for these package dependencies. Some more insight about these packages are :-
🔘 libcanberra-gtk2: Libcanberra is an implementation of the XDG Sound Theme and Name Specifications, for generating event sounds on free desktops, such as GNOME. It comes with several backends (ALSA, PulseAudio, OSS, GStreamer, null) and is designed to be portable.

🔘 packagekit-gtk3-module: PackageKit is a system designed to make installing and updating software on your computer easier. The primary design goal is to unify all the software graphical tools used in different distributions and use some of the latest technology like PolicyKit.

👉here i am installing so much packages at the same time because i want to create an image for dockerhub so that i can pull that image each time when there is need for ML model training.
Now it's time to build the image. For that run the below mentioned command on the same folder where you have the “Dockerfile"
docker build -t <imagename>:<tag> .
we use “.” in last to tell docker that Dockerfile is there where we are running “docker build” command. If you notice here we are not mentioning any file name because I already told you this name of the file “Dockerfile” is fixed. So, on your currently workspace it will look for that file & start building the image from it. After doing this ,docker build will start creating image and it will take some time depend upon your internet speed.

No alt text provided for this image
No alt text provided for this image
🛑BTW you can pull this image for doing any ML task directly from my DockerHub account 👉 docker pull abhi09singh/guidockeriso:v1

STEP-2 : Run any GUI software on the container

Once build is done, let's launch the container. Now we definitely know that Docker Container don't has a gui screen to run the Firefox,jupyter notebook etc. that's why we need to tell the container to use the host system’s gui screen & for that we gonna use that environmental variable using the option “env” in “docker run” command.We will also share the host network driver with container by setting up the argument --net=host . So, run the below mentioned command…
docker run -it --name <name of os> --env="DISPLAY" --net=host <imagename:tag>
No alt text provided for this image
That's all… Now let's see it in action in the below GIF while launching Jupyter notebook and firefox etc…

Launching Jupyter Notebook
Launching Firefox
Now, you can do all pre-processing and analysis stuff and create a model.

Hope so throught this article you got to know something new.

If anybody want to know that how i push the image to my dockerhub repository,here is the detailed link which i followed given below:


Above process is simple and take less than a minute but by doing this you can save time of others and yours as well for any future implementation. see below image where i push my image to my dockerhub account repository for more detail :

No alt text provided for this image
Thankyou for your time for reading 💌

For any queries, corrections, or suggestions you can always connect with me on my LinkedIn.
