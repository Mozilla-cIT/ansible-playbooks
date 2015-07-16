This document assumes you have access to IAM, and know how to do the basics with it. You will need an AWS access ID and secret key, with read-only access. Right now it'll only look at EC2 instances, so that's all it'll have read-only access to.  Do ***not*** use your personal key.


## Setting up the master server

First set up the PPA and install Ansible
```
$ sudo apt-get install software-properties-common
$ sudo apt-add-repository ppa:ansible/ansible3
$ sudo apt-get update
$ sudo apt-get install ansible
```

Next install pip, because we're gonna be doing Python stuff.
```
$ sudo apt-get install python-pip
```

and now boto, the AWS library for Python. We're using this to automagically get servers that are tagged with "Project: communityit". It saves us from having to manually update the hosts file every time a server scales/is created/deleted.

```
$ sudo pip install boto
```

Now, we'll make a configuration file.

Create ```/etc/boto.cfg```, using this template:
```yml
[Credentials]
aws_access_key_id = <your_access_key_here>
aws_secret_access_key = <your_secret_key_here>
```

Remember, **DON'T USE YOUR PERSONAL ACCESS KEYS**


And now finally, we're going to clone our Ansible repo.

```
git clone git@github.com:Mozilla-cIT/ansible-playbooks.git /etc/ansible
```

And from here, the master should be set up.
