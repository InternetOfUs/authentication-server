# Authentication Server

The Authentication Server provides the following main functionality:

1. enabling request authentication in the communication between the various components of the WeNet platform; 
2. enabling request authentication for external applications build on top of the WeNet platform; 
enforcing user authentication;

This component is currently mapping the urls of the components platform, deployed on the infrastructure of the partners responsible for them, to default and static urls.


## Deployment

The deployment and configuration of the service are handled by the Ansible playbook. Kong needs a database to store its configuration and to manage the authentication. So a Postgres database has been added to the deployment. Kong has a series of migrations that should be applied to the database, to do so two other components have been added to the docker-compose: kong-migrations and kong-migrations-up. 
Optionally It is possible to add a dashboard for monitoring and managing kong. In the docker-compose is available the konga service which contains an instance of the opensource Konga dashboard. This dashboard requires a database, so a dedicated Postgres database has been added to docker-compose. Also, the konga-prepare has been added to perform all the migrations 

For running the ansible-playbbok and get a working deployment, first it is necessary to install anisble. Look at the installtion guide [here](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html).


Next install all the required roles:

```sh
ansible-galaxy install -r requirements.yml
```

The next step is prepering you environment: duplicate the `example` directory in the `inventory` folder and fill all the variables.

Finally run the `playbook.yml` script:

```sh
ansible-playbook -i inventory/my_inventory playbook.yml
```