# bigdata-emr-aws

## Introduction

This is a project for the course ST0263 (Special Topics in Telematics) at EAFIT University, in this project we'll provide evidence for the work done in the labs for Unit 3 of the course that focuses on big data.

## Goals
 - Learn how to deploy an EMR Cluster in AWS
 - Learn how to manage datasets and files for the EMR
 - Learn how to persist the data in EMR using S3 Buckets

## Requirements
 - An AWS Account
 - Basic understanding on how the AWS interface works
 - Understandin on how to connect via SSH

## Project Structure
 The project is organized in a way that you can follow along, the first part focuses on how to deploy the EMR Cluster in AWS, then we'll focus on how to enable HUE and the different ways that we can manage files, finally since the instances are terminated, all data will be lost, so to persist the data we'll make use of an AWS S3 Bucket


## Pre-requisites
We'll provide a brief explanation for the following requirements:

- [x] You must create a key pair to be able to connect using ssh, you can also use an existing key pair
- [x] You must create an s3 bucket

### Let's create a key pair:

1. Search for "key pairs" in AWS search bar and click on "Key Pairs" in the features category
    ![key_1](Images/Keys/image%2013key.png)

2. Then click on create key pair and set a name for your key pair
    ![key_2](Images/Keys/image%2014key.png)

After that you must save the key file and you'll be done for now

### S3 Bucket

Creating an s3 bucket is necessary for one of the following steps, in order to do so:

1. Let's search "s3" in the aws searchbar
    ![bucket_1](Images/Bucket/image%2018Bucket.png)

2. Click on create bucket and set a name for the bucket, you'll need to remember this name since we'll use it further in the project
    ![bucket_2](Images/Bucket/image%2019Bucket.png)

3. Let the options as following:
    ![bucket_3](Images/Bucket/image%2020Bucket.png)
    ![bucket_4](Images/Bucket/image%2021Bucket.png)
    ![bucket_5](Images/Bucket/image%2022Bucket.png)    


## How to deploy an AWS EMR Cluster


1. Search for aws EMR and click on the first result
    ![cluster_1](Images/Cluster/image%201cluster.png)

2. Then click on create cluster
    ![cluster_2](Images/Cluster/image%202cluster.png)

3. We'll let the initial screen as default and click on "Go to advanced options"
    ![cluster_3](Images/Cluster/image%203cluster.png)

4. Let's set the version of the emr to emr-6.3.1
    ![cluster_4](Images/Cluster/image%204cluster.png)

5. Then choose only the following options:

- [x] Hadoop 3.2.1
- [x] JupyterHub 1.2.0
- [x] Hive 3.1.0
- [x] Sqoop 1.4.7
- [x] Zeppelin 0.9.0
- [x] Tez 0.9.2
- [x] JupyterEnterpriseGateway 2.1.0
- [x] Hue 4.9.0
- [x] Spark 3.1.1
- [x] Livy 0.7.0
- [x] HCatalog 3.1.2

![cluster_5](Images/Cluster/image%205cluster.png)

6. Edit software configuration with the name of the bucket you setup in previous steps
![cluster_7](Images/Cluster/image%207cluster.png)

7. Enable Glue Data Catalog
![cluster_8](Images/Cluster/image%208cluster.png)

8. The configuration for this step should look something like this:
![cluster_9](Images/Cluster/image%209cluster.png)

9. Click next, and change the instances from m5.xlarge to m4.xlarge
![cluster_10](Images/Cluster/image%2010cluster.png)

10. Also change the instances purchasing option to Spot
![cluster_11](Images/Cluster/image%2011cluster.png)

11. Enable auto-termination
![cluster_12](Images/Cluster/image%2012cluster.png)

12. Set the cluster name
![cluster_16](Images/Cluster/image%2016cluster.png)

13. Click Next and setup your existing key pair
![cluster_15](Images/Cluster/image%2015cluster.png)

14. When you are done, you'll need to wait for about 25 minutes for the cluster to be ready
![cluster_17](Images/Cluster/image%2017cluster.png)

## Security Groups and Ports

1. To setup the security group to the master node, search for security groups in the aws search bar and click on Security Groups EC2 Feature
![sg_25](Images/SG/image%2025SG.png)

2. The choose the master node
![sg_26](Images/SG/image%2026SG.png)

3. Click on edit inbound rules
![sg_27](Images/SG/image%2027SG.png)

4. Then allow access for the following ports
![sg_24](Images/SG/image%2024SG.png)
![sg_23](Images/SG/image%2023SG.png)

5. Finale on the EMR go to block public access settings and update the exceptions
![sg_28](Images/SG/image%2028SG.png)


## File Management Using Hue

1. Go to the cdn address for your cluster with the port enabled for HUE
![hue_35](Images/hue/image%2035hue.png)

2. Create an user
![hue_36](Images/hue/image%2036hue.png)

3. This will redirect you to Hue Dashboard
![hue_37](Images/hue/image%2037hue.png)

4. In the sidebar click on files
![hue_38](Images/hue/image%2038hue.png)

5. Then click on upload and upload the datasets
![hue_39](Images/hue/image%2039hue.png)

### Data persistence using AWS S3   

1. In the sidebar click on s3
![hue_41](Images/hue/image%2041s3.png)

2. Then upload the dataset files
![hue_42](Images/hue/image%2042s3.png)

## File Management Using HDFS CLI via SSH

1. Copy the DNS url in for the master
![hdfs_29](Images/hdfs/image%2029.png)

2. Connect via ssh using your key pair
![hdfs_30](Images/hdfs/image%2030.png)

3. This is how it will look like if you manage to connect
![hdfs_31](Images/hdfs/image%2031.png)

4. Access super user hadoop
![hdfs_32](Images/hdfs/image%2032.png)

5. Copy the datasets into hadoop
![hdfs_33](Images/hdfs/image%2033.png)

6. And check if they were uploaded succesfully
![hdfs_34](Images/hdfs/image%2034.png)

### Data persistence using AWS S3   

1. Copy the files in hadoop to the s3 bucket
![hdfs_34](Images/hdfs/image%2044s3.png)

2. It should show something like this
![hdfs_34](Images/hdfs/image%2045s3.png)

3. You can verify in the bucket
![hdfs_34](Images/hdfs/image%2046s3.png)

## Thanks
That's all.