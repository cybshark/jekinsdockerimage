# Create Jenkinserver Using  Docker Image 

## Problem statement 
1.	Create container image that’s has Jenkins installed  using dockerfile 

2.	When we launch this image, it should automatically starts Jenkins service in the container.

## Software 
Read Hat 8, jenkins , openjdk 11.2 , htppd

## 1.	Create container image that’s has Jenkins installed  using dockerfile 

  #### STEP 1. : Create one directory *jenkins* And create one file name *is Dockerfile*.
'''
[root@localhost ~]# mkdir jenkins
'''

We configure jenkins using centos, First we nedd to download Docker image from the *hub.doker.com*.
Open CLI in readhat And Pull Centos:latest

''''
[root@localhost ~]# docker pull centos 
''''

#### Edit Docker file 

''''
[root@localhost ~]# gedit Dockerfile
''''

![Dockerfile.jpg]()
