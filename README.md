MongoDB
=======

- No Schema

- Download the 64-bit version from: 

http://mongodb.org/downloads

Note: Assume mongo db was extracted at this folder: 

/opt/mongodb-osx-x86_64-2.4.9/bin

- Run Mongo DB server: 

sudo ./mongod

Note: The database will be stored in: /data/db by default

- Run Mongo DB client 

./mongo 

- Mongo DB commands: 

> - db 
> - db.getMongo() 
> - show dbs
> - use [DatabaseName]
> - show collections

- Replica Sets

> - sudo ./mongod --dbpath /data/primaryDB --port 30000 --replSet "demo"
> - sudo ./mongod --dbpath /data/secondaryDB --port 40000 --replSet "demo"
> - sudo ./mongod --dbpath /data/arbiterDB --port 40000 --replSet "demo"

./mongo --port 30000

var demoConfig = {
  _id: "demo", 
  members: [
    {
      _id: 0, 
      host: "localhost:30000",
      priority: 10
    },
    {
      _id: 2, 
      host: "localhost:40000",
    },
    {
      _id: 3, 
      host: "localhost:50000",
      arbiterOnly: true
    }
  ]
}

rs.initiate(demoConfig)

rs.status()

db.test.save({_id:0, value:"hello world!"})

db.test.find()

./mongo --port 40000

db.setSlaveOk()

db.test.find()
