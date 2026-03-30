Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/jammy64" # ubuntu version
  config.vm.hostname = "websrv01" # name of host
  config.vm.network "private_network", ip: "192.168.56.10" # Static IP
  config.vm.network "forwarded_port", guest: 80, host: 8080 # Port forwarding: Windows:8080 -> VM:80
  config.vm.provider "virtualbox" do |vb|
    vb.name   = "vagrant-webserver"   # Virtualbox name
    vb.memory = 1024                  # Memory in MB
    vb.cpus   = 1                     # CPU cores
  end

  config.vm.provision "shell", inline: <<-SHELL
    echo "=== Startar installation ==="

    apt-get update -y             # Update packages
    apt-get install -y apache2    # Install Apache

    systemctl enable apache2      # Run Apache on startup
    systemctl start apache2       # Start Apache

    echo "<h1>Hello World! - Vagrant VM</h1>" > /var/www/html/index.html  # Create a webpage
    echo "=== Installation Complete ==="
  SHELL

end