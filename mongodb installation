# Steps to install MongoDB 6.0 community ediction on Ubuntu 22.04.02 LTS (Jammy distro)

## 1. Import the public key used by the package management system.


From a terminal, issue the following command to import the MongoDB public GPG Key from


    wget -qO - https://www.mongodb.org/static/pgp/server-6.0.asc | sudo apt-key add -

The operation should respond with an "OK".

However, if you receive an error indicating that gnupg is not installed, you can:

### i. Install 'gnupg' and its required libraries using the following command:
    

    sudo apt-get install gnupg


#### ii. Once installed, retry importing the key:

    wget -qO - https://www.mongodb.org/static/pgp/server-6.0.asc | sudo apt-key add -



## 2. Create a list file for MongoDB. 

Create the /etc/apt/sources.list.d/mongodb-org-6.0.list file for Ubuntu 22.04 (Jammy):

    echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/6.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-6.0.list

## 3. Reload local package database.

    sudo apt-get update

## 4. Install the MongoDB package.

    # latest stable version:
    sudo apt-get install -y mongodb-org

## 5. Start or Run the MongoDB instance

    sudo systemct start mongod

    # if you receive error, reload the Daemon
    sudo systemct daemon-reload

## 6. Verify MongoDB has started successfully

    sudo systemctl status mongod

    # stop mongodb
    sudo systemctl stop mongod

    # restart mongodb
    sudo systemctl restart mongod

    # activate mongo shell
    mogosh

## 7. Mongo data and logs directory
    # data Dir
    /var/lib/mongodb

    # logs Dir
    /var/log/mongodb

## 8 UNINSTALLING MongoDB Community Edition

    # stop MongoDB instance
    sudo service mongod stop

    # remove packages
    sudo apt-get purge mongodb-org*

    # remove database and log files
    sudo rm -r /var/log/mongodb
    sudo rm -r /var/lib/mongodb
