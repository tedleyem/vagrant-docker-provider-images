# Vagrant docker provider images 

 This is a list of docker images to build 
 for testing [Vagrant's Docker provider](https://developer.hashicorp.com/vagrant/docs/providers/docker/configuration).
 Used for testing ansible playbooks with Vagrant because ansible molecule
 installation and setup can be cumbersome. 

## Images
* Debian 
* Ubuntu
* CentOS 


## Usage

Update the `docker.image` as required in sample `Vagrantfile`:

### Example

```vagrant
ENV['VAGRANT_DEFAULT_PROVIDER'] = 'docker'

Vagrant.configure("2") do |config|
  config.vm.provider "docker" do |d|
    d.image = "mcwarman/vagrant-provider:alpine"
    d.has_ssh = true
  end
end
```

