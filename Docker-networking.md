Lab Docker Networking 
Task 1: Create a new docker bridge and check connectivity between containers of same bridge
1.	Check the networks available in docker host by ```docker network ls``` command, it displays the default bridge, host and none networks
```
docker network ls
```
2.	Create a new bridge network named ct-bridge1 with the docker network create command
```
 docker network create --driver bridge ct-bridge1
 ```
3.	Inspect the newly created ct-bridge1 bridge network and see the IP address range 
```
docker network inspect ct-bridge1
```
4.	List the docker networks again to see the new network
```
docker network ls
```
5.	Create two containers with name ct-c1 and ct-c2 in the newly created bridge network ct-bridge1 using docker run command with --network option, use busybox image for ct-c1 container
```
docker run -it --network ct-bridge1 --name=ct-c1 busybox
```
6.	Press ‘control+p+q’ to detach the container and switch to shell of docker host

7.	Create second container named ct-c2, using busybox image
```
docker run -it --network ct-bridge1 --name=ct-c2 busybox
```
8.	Press ‘control+p+q’ to detach the container and switch to shell of docker host

9.	Inspect ct-bridge1 network again. See the bridge network now has the details of the two containers created in that network
```
docker network inspect ct-bridge1
```
10.	Check for the running status of two running containers with docker ps command
```
docker ps
```
11.	Attach to the shell of ct-c2 container by docker attach command
```
docker attach ct-c2
```
12.	Ping the ct-c1 container in the same bridge from ct-c2 container using container name and verify that ping gets a reply, hence proving service discovery using container names within same Docker bridge network
```
ip addr
```
```
ping -c 5 ct-c1
```
13.	Press ‘control+p+q’ to detach the container and continue it to run in background
## Task 2: Create a new docker bridge and check connectivity between containers of different bridges
1.	Create a second bridge network named ct-bridge2 with the docker network create command

 

 

2.	Create two containers with the name ct-c3 and ct-c4 with busybox image in ct-bridge2 bridge network by the given commands. Press ‘control+p+q’ to detach the container and to switch to docker host shell

 

3.	Attach to the shell of ct-c4 container by the docker attach command

 

4.	Ping the ct-c3 container in the same bridge from ct-c4 container using container name and verify that ping gets a reply as they are on same bridge network
 
 
              
               
5.	Ping the ct-c1 container and ct-c2 container in the different bridge from ct-c4 container using container name and verify that ping fails to resolve the container names and shows error name or service unknown, hence proves service discovery using container names between docker bridge networks are not possible, hence bridge networks provides complete network isolation for containers

 

 

Task 3: Using ‘Docker network connect’ command create a successful connection between containers of different bridges

1.	Use the network ls command as shown below to see all networks 

 

             

2.	Use the docker network connect command to connect the container ct-c1 to ct-bridge2 network

 

 

3.	Use the docker network inspect command to verify the bridge network to have the container which we configured in step 2.

 

 

 


4.	Since ct-c4 container is already connected to ct-bridge2, there is no need to run a command trying to connect to it; and it is already verified in step 2 above.

5.	Login to ct-c1 container using docker attach command and ping ct-c4 container. Also, use ip addr command to verify the network interfaces associated with ct-c1 container.

 



 


6.	Check the routes configured in ct-c1 container using the ip route command

 

               
Task 4: Launch a container to host network
1.	Press ‘control+p+q’ to detach the container and continue it to run in background

2.	Use the docker run command to start a container ct-c5 with busybox image and using --network option to run it in host network

              
            
3.	Use the command ip addr to view the network interfaces associated with ct-c5 container. Notice the eth0 interface IP address is the same as the virtual machine(host) IP address

 
 

 

4.	Use the command docker network inspect host command to verify the newly created network and the associated container ct-c5

 
 

 
            



Task 5: Launch a container to none network 
1.	Use the docker run command to start a container ct-c6 with busybox image and using --network option to run it in none network

             

2.	Use the command ip addr to view the network interfaces associated with ct-c6 container. Notice there are no IP addresses assigned to the container except for the loopback address 127.0.0.1

             

 

3.	Press ‘control+p+q’ to detach the container and continue it to run in background




