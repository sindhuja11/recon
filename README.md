# Recon

Reconnaisance for Recruitment.

## Getting Started

The project is vagrant-ized. So all you need to do is:

* Install Vagrant
* Clone this repository
* Run `vagrant up` to provision and boot a VM
* Run `vagrant ssh` to login to the VM
* Run `cd /vagrant; rails server -b 0.0.0.0` to start the server
* Hit `localhost:3000` in your browser

## Production Deployment

### Initial Setup

    # Install Docker
    curl -sSL https://get.docker.io | sh

    # Pull and run postgres (needs to be done only once)
    mkdir /var/lib/recon-postgres
    docker pull postgres:9
    docker run --name recon-postgres -v /var/lib/recon-postgres:/var/lib/postgresql/data -d postgres:9

    # Clone the repository
    git clone https://github.com/TWChennai/recon.git

### Build and Run

    # Build the latest Recon (this is going to take quite a bit of time)
    git pull
    docker build -t recon:latest .

    # Remove the old container (if you're redeploying)
    docker stop recon-prod
    docker rm recon-prod

    # Run
    docker run --name recon-prod --link recon-postgres:postgres -p 80:8080 -d recon:latest

## Production Testing in Vagrant

    export RAILS_ENV=production PORT=3000
    docker/start
