Go to the security group on SSH and allow MY Ip to port 22 if you want to SSH

How to log onto SSH:
ssh -i /Users/peteburquette/.ssh/postgres-on-ec2.pem ubuntu@ec2-52-23-111-225.compute-1.amazonaws.com

How to tail the Docker on EC2 to check for errors:

// list of containers, find your container ID
docker ps  

// Tail the containter
docker logs -f <container_id>

Currently: docker logs -f 6eabce660476
PostgreSQL: docker logs -f 7e8e6a257e4e

Note:  It seems like Healthy is  PostgreSQL server of choice

