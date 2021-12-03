# Dockerizing Django with Postgres, Gunicorn, and Nginx



### Development

Uses the default Django development server.

1. Create docker inner network with command: docker network create django_net
1. Rename *.env.dev-sample* to *.env.dev*.
1. Update the environment variables in the *docker-compose.yml* and *.env.dev* files.
1. Change Postgres init.sql file to create custom db and user
1. To start django app you have postrges db listening on 5432 tcp port(NOT inner)
1. Use pgadmin to connect to postgres with postgres service name as dns name
1. Build the images and run the containers:

    ```sh
    $ docker-compose up -d --build
    ```

    Test it out at [http://localhost:8000](http://localhost:8000). The "app" folder is mounted into the container and your code changes apply automatically.

### Production

Uses gunicorn + nginx.

1. Rename *.env.prod-sample* to *.env.prod* and *.env.prod.db-sample* to *.env.prod.db*. Update the environment variables.
1. Build the images and run the containers:

    ```sh
    $ docker-compose -f docker-compose.prod.yml up -d --build
    ```

    Test it out at [http://localhost:1337](http://localhost:1337). No mounted folders. To apply changes, the image must be re-built.


##### Useful docker commands
1. docker-compose logs <service-name> - display inner service logs
1. docker-compose build --no-cache    - command rebuild service from docker-compose from scratch
1. docker-compose up -d --build       - start services in detached mode with building services 
1. docker volume ls                   - list all created volumes
