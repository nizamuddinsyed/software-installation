## How to create self signed ssl certificate?

You can create a self-signed SSL/TLS certificate using OpenSSL, which is a widely used open source tool for working with SSL/TLS certificates.


To create a self-signed SSL/TLS certificate using OpenSSL, you can follow these steps:

Install OpenSSL on your system if it is not already installed. On Ubuntu or Debian-based systems, you can use the following command to install OpenSSL:

    sudo apt-get install openssl
Generate a private key:

    openssl genrsa -out key.pem 2048
This will generate a new 2048-bit private key and save it to a file called key.pem.

Create a certificate signing request (CSR):

    openssl req -new -key key.pem -out csr.pem

This will create a new CSR and save it to a file called csr.pem. You will be prompted to enter some information, such as your organization name and country, during this step.

Generate a self-signed certificate using the private key and CSR:

    openssl x509 -req -in csr.pem -signkey key.pem -out cert.pem

This will create a new self-signed certificate and save it to a file called cert.pem.

You can now use the key.pem and cert.pem files to configure SSL/TLS for your MongoDB instance.


## Configure mongod and mongos for TLS/SSL

    1. Obtain an SSL/TLS certificate and key file from a trusted certificate authority (CA). You can purchase a certificate from a commercial CA or create a self-signed certificate.

    2. Copy the SSL/TLS certificate and key file to the server where MongoDB is installed.

    3. Configure MongoDB to use TLS/SSL by editing the mongod.conf or mongos.conf file and adding the following configuration options:

    net:
        ssl:
            mode: requireSSL       # specifies that TLS/SSL is required for all connections to the MongoDB instance
            PEMKeyFile: /path/to/keyfile.pem    # specifies the path to the SSL/TLS certificate and key file
            PEMKeyPassword: <password>          # specifies the password to unlock the key file
            CAFile: /path/to/cafile.pem         # specifies the path to the CA certificate file used to verify client certificates

    4. Restart the MongoDB service for the changes to take effect.

    5. Verify that MongoDB is using TLS/SSL by connecting to the MongoDB instance using the mongo command and specifying the --ssl option:
        mongo --ssl --host <hostname> --port <port>

        If the connection is successful, you will see a message indicating that you are connected to a TLS/SSL-enabled MongoDB instance.


## How can other users sign in to mongodb with ssl?

    1. Provide the client with a copy of the CA certificate file used to sign the server certificate, as well as any required client certificates.
    2. Instruct the client to connect to the MongoDB instance using the --ssl option, along with the appropriate SSL/TLS options such as the --sslCAFile, --sslPEMKeyFile, and --sslPEMKeyPassword options as needed.
    
    For example, if the client is using the mongo command-line client and has been provided with the CA certificate file and a client certificate file called client.pem, they can connect to the MongoDB instance using the following command:

    mongo --ssl --sslCAFile /path/to/cafile.pem --sslPEMKeyFile /path/to/client.pem --host <hostname> --port <port>
