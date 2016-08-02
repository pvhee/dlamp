### Important commands

1. Install [docker & docker-compose][docs.docker]
1. Create a link to the project: `ln -sfP /srv/d8 www` (or `ln -sf /srv/d8 www` on Mac)
1. Create a link to your credentials: `cp ~/.ssh apache/ssh`
1. Start the project: `docker-compose up -d`
1. Execute commands inside of the container: `docker-compose run drupal-lamp bash`
1. Before shutdown your environment `docker-compose stop`
1. Update all containers: `docker-compose build`

### Extra commands

1. Delete all containers: `docker rm $(docker ps -q -f status=exited)`
1. Delete all images: `docker rmi $(docker images -q)`

#### Footnote

[1] If you change the link `www/` you should reload the containers.

[2] If you want to use symfony use `000-sf.conf` rather the default one

[3] I don't like the idea of copy your SSH inside of the project, but we are
facing dependencies with private repositories, unfortunately.


[docs.docker]: https://docs.docker.com/engine/installation/linux/ubuntulinux/
