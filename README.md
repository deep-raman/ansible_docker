ansible_docker
==============

The roles in this repo creates the redis-cluster, rabbitmq-cluster and mysql-master-slave on Docker.


Playbooks
---------

- **redis_cluser.yaml** : installs the redis cluster on docker containers

- **rabbitmq_cluster.yaml** : installs the rabbitmq cluster

- **mysql_master_slave.yaml**: installs the mysql master-slave replication containers

Variables
---------

To check the default varibles and customize them check the **defaults/main.yml** in each role.


Tags
----

- redis-cluster
	
	  - deploy : tag to deploy redis containers, network, volumes and configure the cluster configuration
	  - cluster: only set up the cluster config, containers must exist
	  - remove_container : removes the containers
	  - remove_volume: remove the persisted volumes
	  - remove_all: removes everything, containers and volumes
	
- rabbitmq-cluster

	  - deploy : creates all the setup containers creation, network, cluster config
	  - cluster : only set up the cluster config, containers must exist
	  - remove_container: removes the containers
	  - remove_volume: remove the persisted volumes
	  - remove_all: removes everything, containers and volumes

- mysql-master-slave
	
	  - deploy: creates the mysql master slave setup
	  - replication: configures only master slave replication between containers, containers must exist
	  - remove_container: removes the containers


Examples 
--------

For the direct one line command installation on localhost use :

- **redis-cluster**
	
	To install redis cluster :
	
		ansible-playbook --connection=local --inventory 127.0.0.1, redis_cluser.yaml --tags deploy
	
	To remove (only) redis containers :
	
		ansible-playbook --connection=local --inventory 127.0.0.1, redis_cluser.yaml --tags remove_container
	
	To remove volumes (this will delete the peristed volumes and cause data loss):
	
		ansible-playbook --connection=local --inventory 127.0.0.1, redis_cluser.yaml --tags remove_volume
		
    To run only cluster configuration :
    
		ansible-playbook --connection=local --inventory 127.0.0.1, redis_cluser.yaml --tags cluster

	
- **rabbitmq-cluster**

	To install rabbitmq cluster :
	
		ansible-playbook --connection=local --inventory 127.0.0.1, rabbitmq_cluster.yaml --tags deploy
	
	To run only cluster configuration:
		
		ansible-playbook --connection=local --inventory 127.0.0.1, rabbitmq_cluster.yaml --tags cluster
		
	To remove only containers:
		
		ansible-playbook --connection=local --inventory 127.0.0.1, rabbitmq_cluster.yaml --tags remove_container
		
	To remove volumes:
	
		ansible-playbook --connection=local --inventory 127.0.0.1, rabbitmq_cluster.yaml --tags remove_volume
	
	To remove remove containers and volumes :
	
		ansible-playbook --connection=local --inventory 127.0.0.1, rabbitmq_cluster.yaml --tags remove_all
		

- **mysql-master-slave**

	To create mysql master slave replcation containers:
	
		ansible-playbook --connection=local --inventory 127.0.0.1,  mysql_master_slave.yaml --tags deploy
	
	To create setup only master-slave configuration:
	
		ansible-playbook --connection=local --inventory 127.0.0.1,  mysql_master_slave.yaml --tags replication
	
	To remove only containers:
		
		ansible-playbook --connection=local --inventory 127.0.0.1, mysql_master_slave.yaml --tags remove_container


Requirements
------------

	- ansible 2.7.7
	- docker 19.03.9

Following additional packages must be installed on the host running docker :

	- python-dockerpty or python-docker-py (depending on the linux distro)
	- PyMySQL (Python 2.7 and Python 3.X) or MySQL-python (Python 2.X)
	- jq


Author Information
------------------

	Raman Deep
	2nd October 2020
	deep.raman85@gmail.com

