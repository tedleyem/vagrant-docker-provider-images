Vagrant.configure("2") do |config|
  # Bug: docker build with vagrant hangs
  # This kills the build process after the images are created creates a false-positive for now 
  config.vm.boot_timeout = 5

  config.vm.define "ubuntu" do |ubuntu|
    ubuntu.vm.provider "docker" do |docker| 
      docker.name = "dev-ubuntu"
      #docker.image = "ubuntu:20.04"
      docker.build_dir = "tests/docker/ubuntu/focal-2004/"
      docker.remains_running = true
      docker.has_ssh = true
      docker.privileged = true
      #docker.volumes = ["/sys/fs/cgroup:/sys/fs/cgroup:rw"]
      # Uncomment to force arm64 for testing images on Intel
      docker.create_args = ["--platform=linux/arm64"]     
    end
  end 

  config.vm.define "debian" do |debian|
    debian.vm.provider "docker" do |docker| 
      docker.name = "dev-ubuntu"
      #docker.image = "ubuntu:20.04"
      docker.build_dir = "tests/docker/debian/bullseye-11/"
      docker.remains_running = true
      docker.has_ssh = true
      docker.privileged = true
      #docker.volumes = ["/sys/fs/cgroup:/sys/fs/cgroup:rw"]
      # Uncomment to force arm64 for testing images on Intel
      docker.create_args = ["--platform=linux/arm64"]     
    end
  end 

  config.vm.define "centos" do |centos|
    centos.vm.provider "docker" do |docker| 
      docker.name = "dev-rhel8"
      #docker.image = "debian:bullseye"
      docker.build_dir = "tests/docker/redhat/rhel8/"
      docker.remains_running = true
      docker.has_ssh = true
      docker.privileged = true
      #docker.volumes = ["/sys/fs/cgroup:/sys/fs/cgroup:rw"]
      # Uncomment to force arm64 for testing images on Intel
      docker.create_args = ["--platform=linux/arm64"]     
    end
  end

  config.vm.define "rhel" do |rhel|
    rhel.vm.provider "docker" do |docker|
      #docker.vagrant_vagrantfile = "tests/host/Vagrantfile"
      docker.name = "dev-rhel8"
      #docker.image = "debian:bullseye"
      docker.build_dir = "tests/docker/redhat/rhel8/"
      docker.remains_running = true
      docker.has_ssh = true
      docker.privileged = true
      #docker.volumes = ["/sys/fs/cgroup:/sys/fs/cgroup:rw"]
      # Uncomment to force arm64 for testing images on Intel
      docker.create_args = ["--platform=linux/arm64"]     
    end
  end

end
