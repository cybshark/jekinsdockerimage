# Create Jenkins server Using  Docker Image 

## Problem statement 
1.	Create container image that’s has Jenkins installed  using dockerfile 

2.	When we launch this image, it should automatically starts Jenkins service in the container.

## Software 
Read Hat 8, jenkins , openjdk 11.2 , htppd

## 1.	Create container image that’s has Jenkins installed  using dockerfile 

 
 #### STEP 1. : Create one directory *jenkins* And create one file name *is Dockerfile*.
~~~
                 [root@localhost ~]# mkdir jenkins
~~~

  We configure jenkins using centos, First we nedd to download Docker image from the *hub.docker.com*.
  Open CLI in readhat And Pull Centos:latest

~~~
                 [root@localhost ~]# docker pull centos 
~~~

#### Edit Docker file 

~~~
                 [root@localhost ~]# gedit Dockerfile
~~~

                 
  ![Dockerfile.jpg](https://github.com/cybshark/jekinsdockerimage/blob/master/jenkins%20image/Dockerfile.JPG)


  Inside docker Container need to wget command working, so first Download wget command, After That Configure Yum repo for jenkins         installation . jenkins work on top of java. In linux openjdk is java rpm to download. After that start to installation of jenkins.
  jenkins is user to need some priviledge to do some operation. so edit sudoers file to give root privildge to jenkins

~~~
              $RUN echo -e "jenkins ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers
              $USER jenkins
              $ENV USER jenkins
~~~
  Jekins work on 8080 port by default , SAve the Docker file.

### STEP 2.: When we launch this image, it should automatically starts Jenkins service in the container.
After Editing script. process to create image. in docker *build* is command to create docker image.
Open CLI And Type
   ~~~
             [root@localhost ~]# docker build -t jenkindoc:v1 /root/jenkins/
   ~~~
   *jenkindoc* is docker image name And after : v1 is version of os you can give any nam */root/jenkins* is path of that floder tere is    Dockerfile are created. its take few minutes. 
   ![buildimage.jpg](https://github.com/cybshark/jekinsdockerimage/blob/master/jenkins%20image/installation%20process.JPG)
   
   After SUCESSFULLY installation done we launch the Docker image using *run* command
   ~~~
                        [root@localhost ~]# docker run  -i -t --name jenkin jenkindoc:v1 
   ~~~
   You can give any name after --name and Enter.
   
   ![runimage.jpg](https://github.com/cybshark/jekinsdockerimage/blob/master/jenkins%20image/launching%20new%20os.JPG)
    
   After that check the of docker imager using *inspect* command. In my scenario my ip is 172.17.0.2 and port is 8080. Open browser and    type http://172.17.0.2:8080 
  
   ![password.jpg](https://github.com/cybshark/jekinsdockerimage/blob/master/jenkins%20image/jenkin%20log%20in.JPG)    
   
   Now we need to enter password here. for password using *cat* command go to above path


   HERE YOUR **JENKINS LOG IN PAGE**
         ![login.jpg](https://github.com/cybshark/jekinsdockerimage/blob/master/jenkins%20image/log%20in.JPG)


[More Details](https://docs.docker.com/get-started/part2/)



Feel free to share your thoughts about the article and in case you run into any problems you can reach me out in [Linkedin](https://www.linkedin.com/in/vishal-dalvi-490b07134/) or email me at v.dalvi404@gmail.com





