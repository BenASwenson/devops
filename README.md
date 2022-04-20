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
    - in Windows be sure to disable Hyper-V in 'Turn Windows Features On and Off'
    - type 'vagrant' in the terminal, run as administrator, to ensure it's correctly installed
    - type 'vagrant --version' 

- install Virtual Box
    - Windows users manually install drivers
        -In File Explorer, navigate to C:\Program Files\Oracle\VirtualBox\drivers\vboxdrv
        -Right click on the VBoxDrv.inf Setup Information file and and select Install
        -When it's finished installing, open up a new terminal window and run sc start vboxdrv
        -Press the Windows Key and search for Control Panel, go from there to Network and Internet, then Network and Sharing Centre, then Change Adapter Settings.
        -Right click on VirtualBox Host-Only Network and choose Properties
        -Click on Install => Service
        -Under Manufacturer choose Oracle Corporation and under Network Service, choose VirtualBox NDIS6 Bridged Networking driver

- Create file 'Vagrantfile' inside your designated project folder
    -paste in the following:

    Vagrant.configure("2") do |config|

        config.vm.box = "ubuntu/xenial64"
    #creating a virtual machine ubuntu
 


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
  - `vagrant up`
  - `vagrant destroy`
  - `vagrant halt`
  - `vagrant reload`
- update `sudo apt-get update -y`
- upgrade `sudo apt-get upgrade -y`
- Who am I `uname` or `uname -a`
- Where am I `pwd`
