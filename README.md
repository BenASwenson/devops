# What is DevOps?
DevOps is a culture which bridges development and operations.  A developer is responsible for new product features, bug fixes, security updates and code refactoring.  After building a project, the development team needs to deploy to a development environment to check for integration and various other aspects of the product.  When deploying from development to production, warning and errors often occur.

Operations teams are responsible for managing servers, ensuring services are running, and that they are sufficiently monitored and growing capacity as the product or company scales and grows.  Operations are met with similar errors and warnings as the development team when deploying development products.

The key aspect of DevOps is to break down the silos that developers and operations work in and have the two teams working closer together, sharing responsibilities, deploying the infrastructure as code, and finally, automating the pipeline throughout.

These principles need to be supported by the engineering practices continuous integration, continuous delivery and continuous deployment, often known as CICD.


## Why Devops
With these DevOps principles in place, greater efficiency enables a faster time to market, improved team collaboration, continuous release cycles, automated scalable environments and increased quality due to automated testing.


### Benefits of DevOps
Bridging development and operations, cross-functional teams to collaborate and resolve, elimate blame culture, release software faster

#### DevOps four key Pillars
- Ease of use
    -Automated pipelines
    -Allows developers to spend more time coding and ensures their work is closer to business intent
- Flexibility
    - The ability to adopt to new market requirements
    - Ability to extend and replace the existing tool sets
- Robustness
    - Iterative approach to design
    - Continuous integration
    - Increased levels of processes automation
    - seamless communication since it unites what were once two seperate teams
- Cost 
    - Initial cost but high ROI
    - Less miscommunication between teams allows for faster delivery 
    - More delivered products = more money

##### Creating Development Environment
- install Ruby

- install Vagrant
    - Vagrant is a tool for building and managing virtual machine environments in a single workflow. With an easy-to-use workflow and focus on automation, Vagrant lowers development environment setup time, increases production parity, and makes the “works on my machine” excuse a relic of the past
    - in Windows be sure to disable Hyper-V in 'Turn Windows Features On and Off'
    - type 'vagrant' in the terminal, run as administrator, to ensure it's correctly installed
    - type 'vagrant --version' 

- install Virtual Box
    - VirtualBox is a general-purpose full virtualizer for x86 hardware, targeted at server, desktop and embedded use
    - Windows users manually install drivers
        -In File Explorer, navigate to C:\Program Files\Oracle\VirtualBox\drivers\vboxdrv
        -Right click on the VBoxDrv.inf Setup Information file and and select Install
        -When it's finished installing, open up a new terminal window and run sc start vboxdrv
        -Press the Windows Key and search for Control Panel, go from there to Network and Internet, then Network and Sharing Centre, then Change Adapter Settings.
        -Right click on VirtualBox Host-Only Network and choose Properties
        -Click on Install => Service
        -Under Manufacturer choose Oracle Corporation and under Network Service, choose VirtualBox NDIS6 Bridged Networking driver

- Create file 'Vagrantfile' inside your designated project folder
    - you can also create this file in your terminal inside project folder with command `vagrant init` 
    -paste in the following:

    Vagrant.configure("2") do |config|

        # creating a virtual machine ubuntu
        config.vm.box = "ubuntu/xenial64"

        # create private network
        config.vm.network "private_network", ip: "192.168.10.100"

        #synced app folder
        config.vm.synced_folder ".", "/home/vagrant/app"

        "Provisioning
        config.trigger.after :up, :provision do |trigger|
        config.vm.provision "shell", path: "provision.sh"
      end
 


    end

- Test installation
    - run 'vagrant up' command from where you have vagrant file available
        - you may see warnings which is normal and you can ignore them for now
    - run 'vagrant status'
    - run 'vagrant ssh'
    - update Ubuntu, type sudo apt-get update

### Linux - Ubuntu distro

- Any tool we use must have admin access
- popular vagrant commands:
  - `vagrant up` #This command creates and configures guest machines according to your Vagrantfile
  - `vagrant destroy` #This command stops the running machine Vagrant is managing and destroys all resources that were created during the machine creation process.
  - `vagrant halt` #This command shuts down the running machine Vagrant is managing
  - `vagrant reload` #The equivalent of running a halt followed by an up.
- update `sudo apt-get update -y`
- upgrade `sudo apt-get upgrade -y`
- Who am I `uname` or `uname -a`
- Where am I `pwd`
- how to check files/folders in existing location `ls` or `ls -a`
- how to create dir `mkdir dir_name`
- navigate to any folder – change dir `cd folder_name`
- how to change back to home location or any location - `cd ..` (one step) or `cd` enter  - to bring you back home
- how to create a file `touch file_name` or `nano file_name`
- To see the content of the file on terminal - `cat file_name`
- How to copy file `cp location_file_name to destination_path`
- cut & paste the file inside the test folder from current location - `mv /location/file_name /location/file_name`
- exit out of nano - `ctrl x enter` or `cntrl x y enter`
- how to delete them `rm -rf folder_name`
- how to check running process in linux `top` or `ps aux`
- how to delete/remove/kill process `kill pid`


### Permissions
- how to check permissions `ll`
- how to switch to `root user` - `sudo su`
- how to change permissions `chmod instruction file_name`
- how to launch a process with time limit of 30sec
  - `timeout DURATION COMMAND` ie `timeout 30s ping www.cyberciti.biz`
- how to delete a process
  - find the process ID (PID) of the program `pidof program_name`
  - kill the process using the PID `sudo kill -9 process_id` or `sudo kill -9 process_id_1 process_id_2 process_id_3` or to kill all processes of a program `sudo kill -9 pidof_program_name`
- How to install a product - install webserver called `nginx`
    - `sudo apt-get install package_name`
- How to check the `status` - `systemctl status nginx`
- create private network with provided ip address - in Vagrantfile add:
  - `config.vm.network "private_network", ip: "192.168.10.100"`

### Bash script - set of commands/instructions from the user to OS
- Provisioning is all tasks related to deployment and configurations of applications making them ready to use.
- Create a .sh called provision.sh `touch provision.sh`
  - `nano provision.sh`
    - fill in file like so:
      - `#!/bin/bash` #the she-bang at the head of the script tells the system this file is a set of commands to be fed to the command interpreter indicated.
      - `sudo apt-get update -y` #downloads the updates of all packages repositories from all configured files or sources.
      - `sudo apt-get upgrade -y` #used to install the newest versions of all packages currently installed on the system
      - `sudo apt-get install nginx -y` #install and configure nginx on Ubuntu
      - `sudo systemctl start nginx` #start the nginx service on a Linux machine
      - `sudo systemctl enable nginx` #marks the unit for auto start at boot time
      - `sudo apt-get install nodejs -y` #NodeJs
      - `sudo apt-get install nodejs=** -y` #NodeJs
      - `sudo apt-get install python-software-properties -y` #NodeJs
      - `curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -` #NodeJs
      - `sudo apt-get install nodejs -y` #NodeJs
- in Vagrantfile, add these lines:
  - `Vagrant.configure("2") do |config|` #The "2" in the first line above represents the version of the configuration object config that will be used for configuration for that block (the section between the do and the end). 
    - #create a virtual machine ubuntu
    - `config.vm.box = "ubuntu/xenial64"`
    - #create a private network with provided ip address
    - `config.vm.network "private_network", ip: "192.168.10.100"`
    - #Synced app folder
    - `config.vm.synced_folder ".", "/home/vagrant/app"`
    - #Provisioners in Vagrant allow you to automatically install software, alter configurations, and more on the machine as part of the vagrant up process
    - `config.trigger.after :up, :provision do |trigger|`
      - `config.vm.provision "shell", path: "provision.sh"`
    - `end`
  - `end`
- Make the file exe - `chmod +x file_name` #executables are used to install or run applications

- Now if we run `vagrant up --provision` VM will be created and nginx url page will be available or `vagrant up` works

### Diagram of Development Environment Process  
  

![] 
(https://miro.medium.com/max/826/1*wt3QFxkSjSZE5CEblJ3QQQ.png)

- Vagrant spins up a virtual machine for you, configures it and installs software on it. All those actions are described in a single text file, called Vagrantfile, that can be shared among team members allowing everyone to have one and the same setup.
- an important reason to use Vagrant is to test how your deployment works, i.e. provisioning, locally before pushing those changes to other environments.
- Other important use cases include the ability to create own development/test environment which is very hard to create on a local machine. 


### Env Variable
- how to check existing `env`, `Env var`, `printenv`
  - access HOME variable `printenv HOME`
- how to print specific env var
- how to create an env var
  - the key word `export`
  - ie `export NAME=Ben` KEY=value
- how to make an env var persistent on linux ubuntu
  - open the current user's profile into a text editor
    - `vi ~/.bash_profile`
  - add the export command for every environment variable you want to persist
    - `export JAVA_HOME=/opt/openjdk11`
  - save your changes
  - to immediately apply all changes to bash_profile, use the source command
    - `source ~/.bash_profile`



### Getting started with deployment / Questions to ask development team
- What are the dependencies required?
- How to run the env tests written in Ruby
- How to transfer/send data from our localhost to our VM
- run the Ruby tests to ensure the dev env has everything needed to deploy the app
- Integration testing - yes/no?
- navigate to spec-tests folder of app and run `gem install bundler` which are required to run Ruby tests
- next run `bundle` to fetch Ruby dependencies
- transfer data from localhost to VM in vagrant with `config.vm.synced_folder ".", "/home/vagrant/app"`
- run tests with `rake spec`
- Failed tests, so go do something to pass them
  - For nginx
    - `vm$ sudo apt-get install nginx -y`
    - `vm$ sudo apt-get upgrade nginx -y`
    - `vm$ sudo systemctl start nginx`
    - `vm$ sudo systemctl enable nginx`
  - For NodeJs
    - `$ sudo apt-get install nodejs -y` won't get us the specified version
      - For specific v6.
        - `vm$ sudo apt-get install nodejs=** -y`
        - `vm$ sudo apt-get install python-software-properties -y`
        - `vm$ curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -`  refer to https://github.com/nodesource/distributions/blob/master/README.md
        - `vm$ sudo apt-get install nodejs -y` | `$ sudo apt-get install -y nodejs` (check)
  - cd app/app, or wherever the deepest app folder is (for now)
    - `vm$ npm install`
    - `vm$ npm start`
    - get the port num {IP}:{port_num} ie `192.168.10.100:3000`
- create .gitignore and ignore node_modules or any dependencies not needed to be pushed to github
