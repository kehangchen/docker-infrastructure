## Local Infrastructure

### Summary

This project will allow developers that have proper computer to create their own development infrastructre without asking help from operation team.  Since it uses the docker engine in the local environment, the environment hosting this will need to allocate enough CPU and memory for the docker engine.  Otherwise, the performance of these running containers will not be good for your development.  If your environment has 4 CPUs and 16 G of memory, you will need to allocate 2 CPUs and 8 G for the docker engine.

### Start Dockers

1. Create a directory to host all the information for different services so even the services restarted can get back to the original state,
``mkdir ~/Documents/data``

2. Modify the docker-compose.yml file to change "kchen" to your user name in your host for every volume paths

3. Start the services with either,
    * detached mode: ``docker-compose up -d``
    * or attached mode: ``docker-compose up``

4. It will take around 5 minutes to have all services up in the ready states.  You can access,
    * Jenkins (http://localhost:9080) - its credential for the first time you access Jenkins can be found in "~/Documents/data/jenkins/secrets/initialAdminPassword" file.  Please note, once you updated the password, this file will be removed.
    * Artifactory (http://localhost:9081) - It will ask for admin password for the first time you access this service
    * SonarQube (http://localhost:9000) - It has the default admin/admin credentials initially
    * Gitlab (http://localhost:9082) - It will ask for new password for root user
    * Docker Registry (http://localhost:9084) - It has no security but it can be easily enabled by setting up a password file.  Will add the instruction later
    * Visualizer (http://localhost:9086) - It is not useful if you are not deploy this docker compose to a docker swarm
    * Consul (http://localhost:8500) - It has no security for now.  Since Vault is using this consul instance as the its backend store, you can access its secret data from this URL after you unseal the vault.

5. Stop the services
``docker-compose down``

### Notes

* If you want to restart everything from the initial state, remove or change the mount volume in the docker-compose.yml as outlined in step 1 above
