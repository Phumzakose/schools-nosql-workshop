# Exploring NoSQL using MongoDB

This is an introduction session using NoSQL databases. We will be using MongoDB.

To get going you will need to install MongoDB using Docker.

## Installing MongoDB using docker

Open a terminal an check if you have docker installed by running the `docker` command.
If you get a command not error you will need to install docker.

Run MongoDB using docker with this command:

```
docker run -d -p 27017:27017 --name mongodb mongo:latest
```

**Note:** this command might take a while to complete as it is downloading a MongoDB container.

To see if mongodb is running using dockor use the `docker ps`. 

You should see mongodb in the list of containers that is running.

You should see something similar to this:

```
CONTAINER ID   IMAGE                              COMMAND                  CREATED        STATUS        PORTS                               NAMES
4d30193839f1   mongo:latest                       "docker-entrypoint.s…"   10 hours ago   Up 10 hours   0.0.0.0:27017->27017/tcp            mongodb
3635e269fca3   mcr.microsoft.com/azure-sql-edge   "/opt/mssql/bin/perm…"   44 hours ago   Up 44 hours   1401/tcp, 0.0.0.0:1433->1433/tcp    trusting_hofstadter
3a672d0f2415   postgres                           "docker-entrypoint.s…"   3 weeks ago    Up 3 weeks    0.0.0.0:5432->5432/tcp              pg-docker
86a5b1214919   mysql:latest                       "docker-entrypoint.s…"   6 weeks ago    Up 6 weeks    0.0.0.0:3306->3306/tcp, 33060/tcp   mysql-docker
```

You should only have one containter at this stage though.

## Run the MongoDB client

We will run the mongodb client inside of the container.

In the command below `mongodb` is the container name and `mongosh` is the MongoDB shell command that we are running inside of the container.

```
docker exec -it mongodb mongosh
```

Next connect to mongodb using: `mongosh`

Once in `mongosh` use the `show dbs` command to see all the databases.

Switch to the schools database using `use schools`. Note your db prompt on the left should change to `schools`. The `show dbs` command will not show the database yet.
It will only be shown once we insert data into the database.

## Create the subject collection

When using MongoDB there is `no need to create tables in advance`. In fact tables are called `collections` and `collections` are created automatically when inserting data into collections.

To create a subject collection just go ahead and insert data into a `subject` collection.

Before we proceed using the `show collections` command to check for collections at this point there should be no collections.

### Create your first collection

To create a `subject` collection just enter the insert command below into the `mongodb` console and press enter

```
db.subject.insertOne({
    _id : 1,
    name : "Mathematics"
});
```

If all goes well you should have 1 entry in the `subject` collection.

You can check using the `show collections` command.

Check that by using this command: `db.subject.find({})`

Go ahead and add more subjects - remember to specify the `_id` & to increment it for each subject:

* Geography
* Life Sciences
* History
* Consumer Studies
* Accounting
* Economics

> **Note:** If you don't specify the id column MongoDB will create a default `_id` column which will be an `ObjectId`.

You can use these commands if needed:

* `db.subject.remove({})` - to remove all subjects
* `db.subject.remove({_id : your_id_here })` - to remove a specific subject id
* `db.subject.find({})` - to find all subjects created