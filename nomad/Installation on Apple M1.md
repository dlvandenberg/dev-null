# Install Nomad
Install the tap:
```bash
$ brew tap hashicorp/tap
```
Install Nomad:
```bash
$ brew install hashicorp/tap/nomad
```

## Other options
[See other options](https://learn.hashicorp.com/tutorials/nomad/get-started-install?in=nomad/get-started)

# Install Vagrant
[[Vagrant]] is a tool for building and managing virtual machines.

Install using homebrew:
```bash
$ brew install vagrant
```

## Other options
[See other options](https://www.vagrantup.com/downloads)

## Configure Vagrant
[[Vagrant]] uses a [[Vagrantfile]] for its configuration. In here you will tell Vagrant what provider and settings to use. 

To quickly setup a new file:
```bash
$ vagrant init
```

See [[Vagrantfile]] for complete configuration options.

## Docker as provider
On Apple M1 there isn't a simple tool to setup a _Virtual Machine_ (VM). However, [[Docker]] can be used also.

Make sure that the [[Vagrantfile]] contains the following _provider_ configuration:

```python
# Custom configuration for docker
config.vm.provider "docker" do |docker, override|
	# docker doesn't use boxes
	override.vm.box = nil
	
	# this is where your Dockerfile lives
	docker.build_dir = "."
	
	# Make sure it sets up ssh with the Dockerfile
	# Vagrant is pretty dependent on ssh
	override.ssh.insert_key = true
	docker.has_ssh = true
	
	# Configure Docker to allow access to more resources
	docker.privileged = true
end
```

This requires a `Dockerfile` to be present in the current directory (`"."`) with the following example content:
```Dockerfile
# Docker image to use with Vagrant
FROM ubuntu:18.04
ENV container docker
RUN apt-get update -y && apt-get dist-upgrade -y

# Install system dependencies, you may not need all of these
RUN apt-get install -y --no-install-recommends ssh sudo libffi-dev systemd openssh-client

# Needed to run systemd
# VOLUME [ "/sys/fs/cgroup" ]
RUN apt-get -y install puppet

# Add vagrant user and key for SSH
RUN useradd --create-home -s /bin/bash vagrant
RUN echo -n 'vagrant:vagrant' | chpasswd
RUN echo 'vagrant ALL = NOPASSWD: ALL' > /etc/sudoers.d/vagrant
RUN chmod 440 /etc/sudoers.d/vagrant
RUN mkdir -p /home/vagrant/.ssh
RUN chmod 700 /home/vagrant/.ssh
RUN echo "ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEA6NF8iallvQVp22WDkTkyrtvp9eWW6A8YVr+kz4TjGYe7gHzIw+niNltGEFHzD8+v1I2YJ6oXevct1YeS0o9HZyN1Q9qgCgzUFtdOKLv6IedplqoPkcmF0aYet2PkEDo3MlTBckFXPITAMzF8dJSIFo9D8HfdOV0IAdx4O7PtixWKn5y2hMNG0zQPyUecp4pzC6kivAIhyfHilFR61RGL+GPXQ2MWZWFYbAGjyiYJnAmCP3NOTd0jMZEnDkbUvxhMmBYSdETk1rRgm+R4LOzFUGaHqHDLKLX+FIPKcF96hrucXzcWyLbIbEgE98OHlnVYCzRdK8jlqm8tehUc9c9WhQ==" > /home/vagrant/.ssh/authorized_keys
RUN chmod 600 /home/vagrant/.ssh/authorized_keys
RUN chown -R vagrant:vagrant /home/vagrant/.ssh
RUN sed -i -e 's/Defaults.*requiretty/#&/' /etc/sudoers
RUN sed -i -e 's/\(UsePAM \)yes/\1 no/' /etc/ssh/sshd_config

  
# Start SSH
RUN mkdir /var/run/sshd
EXPOSE 22
RUN /usr/sbin/sshd

# Start Systemd (systemctl)
CMD ["/lib/systemd/systemd"]
```

# Start Vagrant
From within the directory where the [[Vagrantfile]] is located, run the command:
```bash
$ vagrant up
```

The command should exit normally. You can verify that the VM has started with `vargant status`:
```bash
$ vagrant status

Current machine states:

default                   running (docker)

The container is created and running. You can stop it using
`vagrant halt`, see logs with `vagrant docker-logs`, and
kill/destroy it with `vagrant destroy`.
```

# Start Nomad
It should be possible to start a _SSH_ session in the VM. Run `vagrant ssh` and start the [[Nomad agent]]:
```bash
$ vagrant ssh
$ sudo nomad agent -dev -bind 0.0.0.0 -log-level INFO
```
This will start the agent in both client and server mode. Wait until you see the following line:
```bash
nomad: cluster leadership acquired
```

# Continue the official startup guide
Follow the remaining steps on [this](https://learn.hashicorp.com/tutorials/nomad/get-started-run?in=nomad/get-started) guide.

# Web interface
The Nomad web interface can be reached at: `http://localhost:4646`