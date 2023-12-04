<center> <u> <h1 style="font-size: 50px;">MinIO Setup</h1> </u> </center>

## 1. Task Requirement :  
- To set up an object storage system in a cluster using MinIO.



## 2. Environment details :
- OS: Ubuntu 20.04


## 3. Tools and technologies :

- MinIO - Latest Version (RELEASE.2023-08-16T20-17-30Z)


## 4 . Definition of tools :

- MinIO - It is a software-defined high performance distributed object storage server. You can run MinIO on consumer or enterprise-grade hardware and a variety of operating systems and architectures.



## 5 .  Command for the setup or configuration.

**Node 1:**
docker run -itd --name minio1 --net=host -e MINIO_ROOT_PASSWORD=redhat1234 -e MINIO_ROOT_USER=admin   -p 9000:9000 -p 9090:9090 -v /mnt/disk1:/data docker.io/minio/minio minio server --console-address ":9090" http://minio{1..4}/data



**Node 2:**  
docker run -itd --name minio2 --net=host -e MINIO_ROOT_PASSWORD=redhat1234 -e MINIO_ROOT_USER=admin   -p 9000:9000 -p 9090:9090 -v /mnt/disk2:/data docker.io/minio/minio minio server --console-address ":9090" http://minio{1..4}/data

**Node 3 :**
docker run -itd --name minio3 --net=host -e MINIO_ROOT_PASSWORD=redhat1234 -e MINIO_ROOT_USER=admin   -p 9000:9000 -p 9090:9090 -v /mnt/disk3:/data docker.io/minio/minio minio server --console-address ":9090" http://minio{1..4}/data

**Node 4 :**
 docker run -itd --name minio4 --net=host -e MINIO_ROOT_PASSWORD=redhat1234 -e MINIO_ROOT_USER=admin   -p 9000:9000 -p 9090:9090 -v /mnt/disk4:/data docker.io/minio/minio minio server --console-address ":9090" http://minio{1..4}/data

## Add the below commands for sidekick MiniIO.
 
 #Do host entry of minio1,minio2,minio3,minio4

podman run -itd --name sidekick -p 8080:8080  docker.io/minio/sidekick--health-path=/minio/health/ready --address :8080 http://minio{1...4}:9000

![](commnd.png)
## To check the bucket and object in the bucket.
![](bucket.png)

#To check the metrics of sidekick.
harsh@harsh:~$ curl -v localhost:8080/.prometheus/metrics

## Test cases list






## 6. Reference Link
https://github.com/minio/sidekick

