# Entropy
An innovative energy-aware IT ecosystem for motivating behavioural changes towards the adoption of energy efficient lifestyles
### Prerequisites:
1. Docker (https://docs.docker.com/install/linux/docker-ce/ubuntu/)   
Tip: after installing docker check that your user has permission to run docker commands. To do so add your user to docker group and reboot the virtual machine.
```
sudo groupadd docker
sudo usermod -aG docker your_username
sudo reboot now
```
2. Docker Compose (https://docs.docker.com/compose/install/)  
Check your docker compose installation:
```
docker-compose --version
```
Current installation guide has been created with version ```docker-compose version 1.23.2, build 1110ad01```
### Installation:
1. Create a folder and place into the following docker-compose.yml file:
```
mkdir entropyproject
cd entropyproject
touch  docker-compose.yml
```

The docker-compose.yml file should contain:
```
version: '3'
services:
  # The pub/sub framework
  activemq:
    image: webcenter/activemq
    ports:
     - 8161:8161
    container_name: activemq
    restart: always
  mongo:
    image: mongo
    ports:
     - 27017:27017
    container_name: mongo
    restart: always
  entropy:
    image: entropyproject/entropy:firsttry
    ports:
     - 8080:8080
    container_name: entropy
    restart: always
  entropy-monitoring:
    image: entropyproject/entropy-monitoring:firsttry
    ports:
     - 8082:8082
    container_name: entropy-monitoring
    restart: always
  entropy-recommendation-engine:
    image: entropyproject/entropy-recommendation-engine:firsttry
    ports:
     - 8081:8081
    container_name: entropy-recommendation-engine
    restart: always
```
2. Execute the dockef-compose file
```
docker-compose up -d
```

3. Entropy platform is READY!!! See how easy it is??? Go to http://localhost:8080 to see it!
![](https://github.com/EntropyEcosystem/Entropy/blob/master/images/entropyFirstPage.png)

4. Next step includes creating an account with admin permisions. For that press the 'Select Account option' and create a new account
![](https://github.com/EntropyEcosystem/Entropy/blob/master/images/createaccount1.png)
![](https://github.com/EntropyEcosystem/Entropy/blob/master/images/createaccount2.png)

5. You are very close! Last step is to log into the mongo container and give admin permisions to the user you just created. (Don't worry this only happens the first time :-))
```
docker exec -it mongo bash
>mongo
>use entropy
>db.User.updateOne(
      { "username" : "your_username" },
      { $set: { "isenabled" : true,"isapproved" : true,"userrole" : "ROLE_ADMIN" } }
   );

```

6. Ready to get into the Entropy platform and start registering your areas, sensors etc.
For more info about how to use the Entropy platform please visit our Handbook : https://entropy-platform-handbook.readthedocs.io/en/latest/

If you are developer interested in using the ENTROPY APIs so as to build your application, service or mobile up upon the ENTROPY platform, you will found our wiki page extremely useful:  https://github.com/EntropyEcosystem/Entropy/wiki
### Lead Developers

The following lead developers are responsible for this repository and have admin rights. They can, for example, merge pull requests.

- Eleni Fotopoulou ([@efotopoulou](https://github.com/efotopoulou))
- Anastasios Zafeiropoulos ([@azafeiropoulos](https://github.com/azafeiropoulos))

### Feedback-Chanel

* Please use the GitHub issues to report bugs.
