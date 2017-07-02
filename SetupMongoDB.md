# Setting up Mongo!
Part of Coursera's [Big Data Specialisation](https://www.coursera.org/learn/big-data-integration-processing), offered by University of California, San Diego was a course on introduction to non-structured databases.    
While the course recommended to use [Cloudera](https://www.cloudera.com/downloads/quickstart_vms/5-10.html) for running MongoDB, this repository holds steps to install and run Mongo directly from any Debian based Linux installation

I had to refer a number of blogs and Stack Overflow posts to clear various errors that occurred during the setup process.

- ### Download MongoDB
  The obvious first step is to download the binaries which can be done by executing the command below.   
  `https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-ubuntu1604-X.X.X.tgz`   
  Or one can download directly from this [link](https://www.mongodb.com/download-center#community), after choosing the correct OS.   
  
  Go to the downloaded directory and untar the file   
  `tar xpf /home/harish/myPackages/MongoDB/mongodb-linux-x86_64-ubuntu1604-X.X.X.tgz`   
  
  Once unzipped, let's add the Mongo home to the bashrc file. The path needs to be altered as per your destination.       
  `echo “export MONGODB_HOME=/home/harish/myPackages/MongoDB/mongodb-linux-x86_64-ubuntu1604-X.X.X” >> ~/.bashrc`   
  `echo "export PATH=$MONGODB_HOME/bin:$PATH" >> ~/.bashrc`   
  `source ~/.bashrc`   
  
  If all the steps are successful, the `mongo` command can be run in terminal to open Mongo console.   
  
- ### Create directory and start service
  Create an empty folder which will be used by Mongo to store data while running the service.   
  `mkdir /home/harish/myPackages/MongoDB/databases`
  
  The tweet data in JSON format which we are going to load into the DB is available in this repository `dataDump.tar.gz`.
  Before that, let's start the MongoDB server.   
  `mongod --dbpath /home/harish/myPackages/MongoDB/databases`   
  The dbpath attribute sets the directory which Mongo will use for storing the data - here the folder we specifically created for this purpose.
  
- ### Load the data
  
  Once the server starts, open a new terminal. The ownership of a file needs to be changed to give write access to the current user while loading the data.   
  `chown 'harish' /tmp/mongodb-27017.sock`   
  Untar the `dataDump.tar.gz` to some location.   
  `mongorestore /home/harish/myPackages/MongoDB/dataDump`   
  will convert the JSON data and store it in the `databases` directory.
  
  Once successful, the server can be shutdown   
  `mongod --dbpath /home/harish/myPackages/MongoDB/databases --shutdown`   
