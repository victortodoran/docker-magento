## Recognition
Shout-out to @lillik and @marius-grad who initially built this repo.
I just added minor adjustments for maintenance and personal use.

## Requirements

This project requiresDocker and Docker Compose installed on the machine. Please follow the Docker installation steps from https://docs.docker.com/engine/installation/ and docker compose installation steps from https://docs.docker.com/compose/install/.

## Installation

Please follow the next steps:
1. Download or clone this project in the directory you want to have the project installed.
2. Open the file `auth.json` from directory .composer and add your [repo.magento.com](http://devdocs.magento.com/guides/v2.0/install-gde/prereq/connect-auth.html) credentials

            "username": "YOUR_USERNAME_USED_ON_REPO_MAGENTO",
            "password": "YOUR_PASSWORD_USED_ON_REPO_MAGENTO"

3. Open a terminal that allows you to run Docker Compose CLI application.
4. Change directory in terminal to the directory where the step 1 was performed.
5. Build the docker images with next command:

`docker-compose up -d --build app`

6. Download and install Magento CE 2 with next command

`docker-compose run setup`

7. Add the next text in hosts file of your OS system:

`172.20.0.5 sandbox.local`

8. Open the browser and type the next link: http://sandbox.local/

## Network IPs ##
| Container | IP |
|--------|--------|
|M2 NGINX|172.20.0.2|
|M2 PHP|172.20.0.3|
|M2 MySQl|172.20.0.4|
|M2 Redis|172.20.0.5|
|M2 Memcached|172.20.0.6|
|M2 Mailcatcher|172.20.0.7|
|M2 Elaticsearch01|172.20.0.8|
|M2 Kibana|172.20.0.9|
|M2 Logstash|172.20.0.10|


## Enter magento(PHP) container to run commands
`docker-compose exec -u www-data phpfpm bash`
