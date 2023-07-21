# edgedb
edgedb example using docker-compose


```console
ziadh@Ziads-MacBook-Air edgedb % pwd                           
/Users/ziadh/Desktop/work/databases/edgedb
ziadh@Ziads-MacBook-Air edgedb % tree -I "edgedb-data|dbschema"
.
└── docker-compose.yml

0 directories, 1 file
```

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