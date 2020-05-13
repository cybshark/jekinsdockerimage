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

                 
  ![Dockerfile.jpg](https://github.com/cybshark/jenkins/blob/master/jenkins%20image/Dockerfile.JPG)


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
   
   ![runimage.jpg](https://github.com/cybshark/jenkins/blob/master/jenkins%20image/launching%20new%20os.JPG)
    
   After that check the of docker imager using *inspect* command. In my scenario my ip is 172.17.0.2 and port is 8080. Open browser and    type http://172.17.0.2:8080 
  
   ![password.jpg](https://github.com/cybshark/jenkins/blob/master/jenkins%20image/jenkin%20log%20in.JPG)    
   
   Now we need to enter password here. for password using *cat* command go to above path


   HERE YOUR **JENKINS LOG IN PAGE**
         ![login.jpg](https://github.com/cybshark/jenkins/blob/master/jenkins%20image/log%20in.JPG)


   Markup : [More Details](https://docs.docker.com/get-started/part2/)

## Job1: Pull the Github repo automatically when some developers push the repo to Github.

  Markup : ![github.jpg]()

We use Poll SCM to trigger this job meaning every 1 min jenkins check update and  push to this repo, Job1 will clone the repo and copy the  Developer file into ``/webage/`` folder.

![pollscm.jpg]()

## Job2: By looking at the code or program file, Jenkins should automatically start the respective language interpreter install image container to deploy code. Here my code is of HTML, hence Jenkins should start the container that has HTML already installed.

Job to is Downstream of job one Means when job 1 run Sucessfully job to start run Automatically.

 ![pollscm.jpg]()

We Create one **python** Code for the Run perticular server. for refrence ```https://www.w3schools.com/python/python_conditions.asp```

 ![Script.jpg]()

After Run python code its start perticular server.

## Job3: Test your app if it is working or not.If the app is not working, then send an email to the developer with error messages.
Here using curl command we check page working or not http_code show the status code, If status code =200 means ist working fine excute the job. But status code Not equal to 200 then its run the python file. for sedding the mail.

![job4shell.jpg]()
 
 ### How to send notification on mail ?
 
  Markup : * Using Email noffication Pluging 
           * Configure any programming languages and run
           
  In my case I Create pythone file to send the notification on mail.
  ```# Python code to illustrate Sending mail from  
# your Gmail account  
import smtplib 
  
# creates SMTP session 
s = smtplib.SMTP('smtp.gmail.com', 587) 
  
# start TLS for security 
s.starttls() 
  
# Authentication 
s.login("sender@gmail.com", "password") 
  
# message to be sent 
message = "SERver Error log ,Check details http://192.168.159.129:8080/job/Job%204/1/console"
  
# sending the mail 
s.sendmail("sender@gmail.com", "reciver@gmail.com", message) 
  
# terminating the session 
s.quit()
```
  
 Finally Mail is here, Inside mail given link, you can test serverlog.  
  ![job4shell.jpg]()
  
  We used here Build Pipeline, its show graphically your job status. 
 ![job4shell.jpg]()
 
 ## Job5: Create One extra job not belonging to the pipeline to monitor: If the container where the app is running. fails due to any reason then this job should automatically start the container again.
 
Some case server goes down we can not run manually here, we create one job for monitoring it, 
if any case sever goes down its restart it.

![job4shell.jpg]()

## Scope this technology
    1. Automation is need is important for any Orgnazation for reduces Human error as well as increase the production.
       DevOps is one technology to fullfill this requirement. 
       
       
       
       
       



 
 
Feel free to share your thoughts about the article and in case you run into any problems you can reach me out in [Linkedin](https://www.linkedin.com/in/vishal-dalvi-490b07134/) or email me at v.dalvi404@gmail.com






