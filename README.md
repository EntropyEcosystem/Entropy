# Entropy
An innovative energy-aware IT ecosystem for motivating behavioural changes towards the adoption of energy efficient lifestyles
### Prerequisites:
1. Docker (https://docs.docker.com/install/linux/docker-ce/ubuntu/)
2. Docker Compose (https://docs.docker.com/compose/install/
Tip: after installing docker check that your user has permission to run docker commands. To do so add your user to docker group and reboot the virtual machine.
```
sudo groupadd docker
sudo usermod -aG docker your_username
sudo reboot now
```
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
