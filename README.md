🐳 edgedb Example
-----------------
edgedb example using docker-compose

🚨 Disclaimer
----------
I am running the following example on `MacBook Air M1` so I might use both `docker compose` and `docker-compose` it is only avaliable on M1 as far as I know.

🔧 Prerequisites
----------------
- [X] Docker Desktop
```console
ziadh@Ziads-MacBook-Air edgedb % docker --version
Docker version 20.10.16, build aa7e414
ziadh@Ziads-MacBook-Air edgedb % docker-compose --version
docker-compose version 1.29.2, build 5becea4c
```

🤓 Example
----------
Create a `docker-compose.yml` file inside an empty directory:
```console
ziadh@Ziads-MacBook-Air edgedb % pwd                           
/Users/ziadh/Desktop/work/databases/edgedb
ziadh@Ziads-MacBook-Air edgedb % tree -I "edgedb-data|dbschema"
.
└── docker-compose.yml

0 directories, 1 file
```
Contents of the file:
```yml
version: "3"
services:
  edgedb:
    image: edgedb/edgedb
    container_name: edgedb
    environment:
      EDGEDB_SERVER_SECURITY: insecure_dev_mode
    volumes:
      - "./dbschema:/dbschema"
      - "./edgedb-data:/var/lib/edgedb/data"
    ports:
      - "5656:5656"
```
Open your favv terminal in the same directory:
```console
ziadh@Ziads-MacBook-Air edgedb % docker-compose ps  
Name   Command   State   Ports
------------------------------
ziadh@Ziads-MacBook-Air edgedb % docker-compose up --build -d
Creating network "edgedb_default" with the default driver
Creating edgedb ... done
ziadh@Ziads-MacBook-Air edgedb % docker-compose ps           
 Name               Command               State           Ports         
------------------------------------------------------------------------
edgedb   docker-entrypoint.sh edged ...   Up      0.0.0.0:5656->5656/tcp
ziadh@Ziads-MacBook-Air edgedb % docker compose exec -it edgedb bash
root@deb15394678b:/# su edgedb
edgedb@deb15394678b:/$ ls
bin   dbschema	etc   lib    mnt  proc	run   srv  tmp	var
boot  dev	home  media  opt  root	sbin  sys  usr
edgedb@deb15394678b:/$ cd dbschema/
edgedb@deb15394678b:/dbschema$ ls
edgedb@deb15394678b:/dbschema$ edgedb project init
No `edgedb.toml` found in `/dbschema` or above
Do you want to initialize a new project? [Y/n]
> Y
Specify the name of EdgeDB instance to use with this project [default: dbschema]: 
> dbschema
Checking EdgeDB versions...
Specify the version of EdgeDB to use with this project [default: 3.1]: 
> 3.1
┌─────────────────────┬───────────────────────┐
│ Project directory   │ /dbschema             │
│ Project config      │ /dbschema/edgedb.toml │
│ Schema dir (empty)  │ /dbschema/dbschema    │
│ Installation method │ portable package      │
│ Version             │ 3.1+8e7e494           │
│ Instance name       │ dbschema              │
└─────────────────────┴───────────────────────┘
[2023-07-21T01:23:51Z WARN  edgedb::portable::local] Error checking port [::1]:10700: Cannot assign requested address (os error 99)
Downloading package...
00:00:19 [====================] 39.08 MiB/39.08 MiB 2.03 MiB/s | ETA: 0s       Successfully installed 3.1+8e7e494
Initializing EdgeDB instance...
[2023-07-21T01:24:28Z WARN  edgedb::portable::project] Error running EdgeDB as a service: either systemctl is not found or environment is wrong
EdgeDB will not start on next login. Trying to start database in the background...
Applying migrations...
Everything is up to date. Revision initial
Project initialized.
To connect to dbschema, run `edgedb`
edgedb@173fc0d1b4ff:/dbschema$ edgedb
EdgeDB 3.1+8e7e494 (repl 3.4.0+c7845b2)
Type \help for help, \quit to quit.
edgedb> \quit
edgedb@deb15394678b:/dbschema$
edgedb@deb15394678b:/dbschema$ ls
dbschema  edgedb.toml
edgedb@deb15394678b:/dbschema$ exit
exit
root@deb15394678b:/# exit
exit
ziadh@Ziads-MacBook-Air edgedb % tree -I "edgedb-data"              
.
├── dbschema
│   ├── dbschema
│   │   ├── default.esdl
│   │   └── migrations
│   └── edgedb.toml
└── docker-compose.yml

3 directories, 3 files
ziadh@Ziads-MacBook-Air edgedb % 
```

# 🍽️ Contrbutions
-----------------
Feel free to fork and pull request to add documentation 📝.
