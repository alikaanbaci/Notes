### CREATING ROOT USER

    $ use admin
    $ db.createUser({
      user: "root",
      pwd: "root123",
      roles : [{role: "root", db: "admin"}]
      })
  
# CONNECT AS A ROOT ANY USER TYPE

    $ mongo --username root --password root123 --authenticationDatabase admin

# SETTING REPLICA SET

     Config file
    	storage:
          dbPath: /var/mongodb/db/node1
    	net:
    	  bindIp: 192.168.103.100,localhost
    	  port: 27011
    	security:
    	  authorization: enabled
    	  keyFile: /var/mongodb/pki/m103-keyfile
    	systemLog:
    	  destination: file
    	  path: /var/mongodb/db/node1/mongod.log
    	  logAppend: true
    	processManagement:
    	  fork: true
    	replication:
    	  replSetName: m103-example

> initiate replica set
    
    $ rs.initiate()

> add replica set
    
    $ rs.add("hostnameofreplset:port")

> change replica set configs

     $ cfg = rs.conf()	

     $ cfg.members[3].votes = 0
     $ cfg.members[3].hidden = true
     $ cfg.members[3].priority = 0

     $ rs.reconfig(cfg)
 
 
 # WRITE CONCERN
 
     $ db.insert({...}, writeConcern: {w: "0"})
     $ db.insert({...}, writeConcern: {w: "1"})
     $ db.insert({...}, writeConcern: {w: "2,3,4.."})
     $ db.insert({...}, writeConcern: {w: "majority"})
     $ db.insert({...}, writeConcern: {w: "majority", wtimeout: 60})
 
 # READ CONCERN
 
   - local -> returns most recent data (for primary)
   - available -> returns most recent data (for secodary)
   - majority
   - linearizble

 	$ db.products.find({...}).readConcern(level: "majority")
 
 
 # CONFIG SERVER SET UP FOR SHARDING
 
 > Configuration file for config serversharding:
 	
    sharding:
	  clusterRole: configsvr
	replication:
	  replSetName: m103-csrs
	security:
	  keyFile: /var/mongodb/pki/m103-keyfile
	net:
	  bindIp: localhost,192.168.103.100
	  port: 26001
	systemLog:
	  destination: file
	  path: /var/mongodb/db/csrs1.log
	  logAppend: true	
	processManagement:
	  fork: true
	storage:
	  dbPath: /var/mongodb/db/csrs1

 > Start as a mongod process
	
     $ mongod --config rsrs_1.conf

 >Connoect with mongo

     $ mongo --port 26001
 
 > create root user and then initiate replica set
 
     $ rs.initiate()
 
 > start to other config server replicas and add to the replica set
 
     $ rs.add("repl_set_name/host_name:port_number")
 
 # CREATE MONGOS PROCESS TO SHARDING
 
 > mongos.conf file
 > 
	 sharding:
	  configDB: m103-csrs/192.168.103.100:26001
	security:
	  keyFile: /var/mongodb/pki/m103-keyfile
	net:
	  bindIp: localhost,192.168.103.100
	  port: 26000
	systemLog:
	  destination: file
	  path: /var/mongodb/db/mongos.log
	  logAppend: true
	processManagement:
	  fork: true

 > shut down mongod replicas respectively and add this to the config file and restart mongod
 
	sharding:
	  clusterRole: shardsvr
	storage:
	  wiredTiger:
		 engineConfig:
		    cacheSizeGB: .1

> start mongos process
  
    $ mongos --config mongos.conf
    
> connect mongos with mongo
  
    $ mongo --port 26000 --username m103-admin --password m103-pass --authenticationDatabase admin
  
> add primary shard
  
    $ sh.addShard("m103-repl/192.168.103.100:27001")

 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
