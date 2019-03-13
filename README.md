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
|Magento 2 NGINX|172.20.0.5|
|Magento 2 PHP|172.20.0.6|
|Magento 2 MySQl|172.20.0.7|
|Magento 2 Redis|172.20.0.8|

## How to use composer application

In order to run composer commands you need to be in the directory of the project(where this docker compose file is used) and type this:

`docker-compose exec -u www-data phpfpm composer [composer CLI options]`

Example of composer update command:

`docker-compose exec -u www-data phpfpm composer update`

## How to use Magento 2 CLI

The next command can be used in the directory of the project (where this docker compose file is used):

`docker-compose exec phpfpm magento [magento CLI options]`


## Suggestions
Try using CLI aliases for the composer and magento.

Example for linux Mint:

 1. Open the __.bashrc__ file
 2. Add the next text at the end of the file:

`alias magento-cli='docker-compose exec phpfpm magento'`

`alias composer='docker-compose exec -u www-data phpfpm composer'`

 3. Restart or open again the terminal window.
 4. Change directory to project location.
 5. Run `composer` or `magento-cli` commands.
 
 
