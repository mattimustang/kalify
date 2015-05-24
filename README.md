Kalify
======

**Automate your Penetration Testing toolchain.**

Meet Kalify
-----------
* Use a single command to set up a new server running Kali Linux.
* New servers can be created at [Amazon EC2](https://aws.amazon.com/ec2/), more
  to come...
* Select from a range of [Kali Linux
  Metapackages](https://www.kali.org/news/kali-linux-metapackages/) to install.
* Have a Kali Linux server up and running in a hour (depending on selected
  metapackage), ready for your next penetration testing engagement.

Installation
------------

### Prerequisites ###
* Kalify requires a BSD, Linux, or OS X system. All of the following
  commands should be run inside a Terminal session.
* Python 2.7 is required. This comes standard on OS X, and is the default on
  almost all Linux and BSD distributions as well. If your distribution packages
Python 3 instead, you will need to install version 2.7 in order for Kalify
to work properly.
* Make sure an SSH key is present in ~/.ssh/id\_rsa.pub.
  * If you do not have an SSH key, you can generate one by using this command
    and following the defaults:

            ssh-keygen
* Install Git.
  * On Debian and Ubuntu

            sudo apt-get install git
  * On Fedora

            sudo yum install git
  * On OS X (via [Homebrew](http://brew.sh/))

            brew install git
* Install the [pip](https://pip.pypa.io/en/latest/) package management system
  for Python.
  * On Debian and Ubuntu (also installs the dependencies that are necessary to
    build Ansible)

            sudo apt-get install python-pip python-dev build-essential
  * On Fedora

            sudo yum install python-pip
  * On OS X

            sudo easy_install pip
* Install [Ansible](http://www.ansible.com/home). If you have an existing
  installation, please note that Ansible version 1.8.2 or higher is required.
  * On OS X (via [Homebrew](http://brew.sh/))

            brew install ansible
  * On OS X Mavericks (via pip)

            sudo CFLAGS=-Qunused-arguments CPPFLAGS=-Qunused-arguments pip install ansible
  * On BSD, Linux, or earlier versions of OS X (via pip)

            sudo pip install ansible
* Install the necessary Python libraries for your chosen cloud provider if you
  are going to take advantage of Kalify's ability to create new servers
  using a supported API.
  * Amazon EC2

            sudo pip install boto
    * You will also need to subscribe to Kali Linux on the [AWS
      Marketplace](https://aws.amazon.com/marketplace/pp/B00HW50E0M). There is
      no cost associated with doing this.
    * You can put your AWS API keys in
      [~/.boto](http://boto.readthedocs.org/en/latest/boto_config_tut.html) to
      save you entering them each time you run Kalify.
    * Amazon does not allow penetration testing to be performed using
      `m1.small` or `t1.micro` instances. However, for testing purposes I have
      set the instance type to `t1.micro`. Edit
      `playbooks/roles/genesis-amazon/defaults/main.yml` and change the
      `aws_instance_type` setting to one of your choosing. I would recommend
      starting with `m1.medium`.
  * If you are using a Homebrew-installed version of Python you should also run
    these commands to make sure it can find the necessary libraries:

            mkdir -p ~/Library/Python/2.7/lib/python/site-packages
            echo '/usr/local/lib/python2.7/site-packages' > ~/Library/Python/2.7/lib/python/site-packages/homebrew.pth

### Execution ###
1. Clone the Kalify repository and enter the directory.

        git clone https://github.com/mattimustang/kalify.git && cd kalify
2. Execute the Kalify script.

        ./kalify
3. Follow the prompts to choose your provider, the physical region for the
   server, and its name. You will also be asked to enter API information.
4. Wait for the setup to complete (this usually takes around one hour for
   a standard install).
5. Connect to your new Kali Linux server.

        ssh admin@[ip address]

The servers should be accessible using your SSH keys, and *admin* is used as the
connecting user by default.

### Obtain Permission ###
Before you go ahead and start scanning the whole Internet with your Kali
Linux server you need to get permission from your target *and* cloud provider. Most cloud
providers have a form that must be completed and a few days turn-around:
* [Amazon EC2 Penetration
  Testing](http://aws.amazon.com/security/penetration-testing/)

Roles
-----
Kalify comes with a growing range of roles that can be used to installed and
configure common security assessment tools. These roles can be applied to you
newly built Kali Linux server by running:

        ansible-playbook playbooks/<role>.yml

The roles available are:
- metasploit
- nexpose
- nessus
- openvas

See the README in each role's directory for more information.

Upcoming Features
-----------------
* Native support for more cloud providers and other Kali Linux installations.
* Easier customization of instance parameters without having to edit the roles.

If there is something that you think Kalify should do, or if you find a bug
in its documentation or execution, please file a report on the [Issue
Tracker](https://github.com/mattimustang/kalify/issues).

Acknowledgements
----------------
I would like to thank Joshua Lund for 
[Streisand](https://github.com/jlund/streisand) which I used to both learn
ansible and as the basis for Kalify.
