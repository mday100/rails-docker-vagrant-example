[![Build Status](https://travis-ci.org/mday100/rails-docker-vagrant-example.svg)](https://travis-ci.org/mday100/rails-docker-vagrant-example)

# Edit Code Locally => Test/Execute in Vagrant against Docker

###

# Spin up Vagrant Ubuntu box running Docker

from the root of this directory run `vagrant up`

# Apply Chef / Shell directives located in Vagrantfile
``` shell
vagrant provision
```
# login to Ubuntu box that Vagrant has created
``` shell
vagrant ssh
cd /app
```
If you run an `ls` command in ~/app, you'll see that code has been shared via directives in Vagrantfile NFS.


# Build new docker image from Dockerfile named demo
``` shell
docker build -t demo . #where demo is the name of the image you are building.
```

# Start docker container named demo_container from the image named demo
``` shell
docker run -dP --name demo_container -p 3000:3000 demo
```

# See docker container named docker_container is a running docker process
``` shell
docker ps
```

# Setup the DB for running RSpec
``` shell
docker exec app_web_1 bin/rake db:migrate
```

# Run RSpec inside of the container against the DB
``` shell
docker exec app_web_1 bin/bundle exec rspec
```
app_web_1 bin/rake db:migrate RAILS_ENV=development
```
# From your Host computer, you should be able to access the Rails app @ http://localhost:1234/