# Vagrant config block, API version "2" (current syntax standard).
# "do" opens a code block closed by "end" at the bottom of the file.
# |config| is our chosen variable name for the configuration object
Vagrant.configure("2") do |config|

  # config = our config variable, .vm = virtual machine, .box = which OS image to use.
  # Downloaded from Vagrant Cloud automatically on first "vagrant up"
  config.vm.box = "ubuntu/jammy64"

  # Sets the hostname inside the VM, shown in terminal as "vagrant@websrv01"
  config.vm.hostname = "websrv01"

  # Adds a Host-only network adapter, a private connection only between Windows and the VM.
  # "ip:" assigns a static IP so the address is always the same
  config.vm.network "private_network", ip: "192.168.56.10"

  # Forwards Windows port 8080 (host) to VM port 80 (guest),
  # so http://localhost:8080 reaches Apache in the VM
  config.vm.network "forwarded_port", guest: 80, host: 8080

  # Configures VirtualBox as the virtualization software.
  # "do |vb|" opens a new block where "vb" is our chosen variable for VirtualBox settings
  config.vm.provider "virtualbox" do |vb|
    vb.name   = "vagrant-webserver"   # Display name in VirtualBox GUI
    vb.memory = 1024                  # RAM in MB (1024 = 1 GB)
    vb.cpus   = 1                     # CPU cores allocated to the VM
  end                                 # Closes the "do |vb|" block

  # Runs this script inside the VM automatically on first "vagrant up".
  # "shell" = run in bash (Linux terminal), "inline:" = script written here
  config.vm.provision "shell", inline: <<-SHELL
    apt-get update -y             # Refresh available packages, -y = auto-confirm
    apt-get install -y apache2    # Install Apache web server

    systemctl enable apache2      # Auto-start Apache on every boot (systemctl = Linux service manager)
    systemctl start apache2       # Start Apache now

    echo "<h1>helloworld! - Vagrant VM</h1>" > /var/www/html/index.html  # Create custom web page, ">" overwrites the file
  SHELL

end  # Closes the "do |config|" block from line 1
