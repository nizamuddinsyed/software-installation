# Authentication
### Authentication is the process of verifying the identity of a client. 
    - Authentication verifies the identity of a user.
    - Authorization determines the verified user's access to resources and operations.

To configure MongoDB for remote access, follow these steps:

Edit the MongoDB configuration file located at 
    
    /etc/mongod.conf (or equivalent)

    Uncomment the line "bindIp: 127.0.0.1" and change it to "bindIp: 0.0.0.0".
    
    # Restart MongoDB for the changes to take effect.
    sudo systemctl restart mongod
    
    # Add firewall rules to allow incoming connections on the MongoDB port (27017 by default).
    
    sudo ufw allow from <IP_ADDRESS> to any port 27017
    sudo ufw enable

    sudo ufw allow 27017/tcp
    sudo ufw enable


    
    # Connect to MongoDB from a remote host using the following command: "mongo <host>:<port>"
    mongo 192.168.1.73:27017


    # iptables on linux
    # It is used to define rules for incoming and outgoing network traffic based on IP address, port number, protocol, and other criteria.

    sudo iptables -A INPUT -p tcp --dport 27017 -j ACCEPT
    iptables -A INPUT -p tcp --dport 27017 -j LOG --log-prefix "MongoDB Access: "

    sudo iptables-save

    # add authentication while logging
    Edit '/etc/mongod.conf', uncomment 'security' section

    security:
        authorization: enabled



### Create admin user
    1. Connect to mongodb

    mongo

    2. Switch to 'admin' database

    use admin

    3. Create a new user

    db.createUser(
    {
        user: "admin", // replace this with admin name
        pwd: passwordPrompt(), // or cleartext password
        roles: [
        { role: "userAdminAnyDatabase", db: "admin" },
        { role: "readWriteAnyDatabase", db: "admin" }
        ]
    }
    )

    4. grant rules on collection level

    db.grantRolesToUser("<username>", 
        [ { role: "<role>",
            db: "<database>",
            collection: "<collection>" 
        } ])

    5. How to create a new database and grant access to user
    
    mongo
    use testdb
    db.createUser({
      user: "nizam",
      pwd: "****",
      roles: [ { role: "readWrite", db: "daquai_db" } ]
    })

    another user:

    db.createUser({
      user: "amartya",
      pwd: "*****",
      roles: [ { role: "readWrite", db: "daquai_db" } ]
    })

    Update User roles

    db.updateUser("testUser", { roles: [{ role: "readWrite", db: "otherdb" }]})


### Command to login to mongodb running on remote server

    mongo 192.168.1.73:27017 --authenticationDatabase "daquai_db" -u "nizam" -p

### Mongo operations

    1. Create new database
        use <database_name>

    2. db.testcollection.insert({ name: "John Doe", age: 30 })

    3. find records
    db.testcollection.find()


mongodb://nizam:1.*****.2!@192.168.1.73:27017/daquai_db?ssl=true
