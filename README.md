# A Virtual Machine for working on a Jekyll blog 


## Kudos

A modified version of <https://github.com/rails/rails-dev-box>

## Requirements

* [VirtualBox](https://www.virtualbox.org)

* [Vagrant](http://vagrantup.com)

## How To Build The Virtual Machine


Building the virtual machine is this easy:

    host $ git clone https://github.com/luciano-fiandesio/jekyll-box.git
    host $ cd jekyll-box


Create a file named `vagrant.yaml`

    host $ touch vagrant.yaml

Add to the `vagrant.yaml` a variable named `host_blog_folder` pointing to your host's blog folder. Example:

    host_blog_folder: "~/blogs/personal-blog"

Start the VM

    host $ vagrant up


After the installation has finished, you can access the virtual machine with

    host $ vagrant ssh
    Welcome to Ubuntu 17.04 (GNU/Linux 4.10.0-21-generic x86_64)
    ...
    ubuntu@rails-dev-box:~$

Access your blog directory, using `cd /blog`

Port 4000 in the host computer is forwarded to port 4000 in the virtual machine. Thus, jekyll server running in the virtual machine can be accessed via localhost:4000 in the host computer. Be sure the web server is bound to the IP 0.0.0.0, instead of 127.0.0.1, so it can access all interfaces. In `_config.yml`

    host: 0.0.0.0

## What's In The Box

* Development tools

* Git

* Ruby 2.4

* Jekyll

* Bundler

* An ExecJS runtime

## Recommended Workflow

The Vagrant file ma
The recommended workflow is

* edit in the host computer and

* test within the virtual machine.

## Virtual Machine Management

When done just log out with `^D` and suspend the virtual machine

    host $ vagrant suspend

then, resume to hack again

    host $ vagrant resume

Run

    host $ vagrant halt

to shutdown the virtual machine, and

    host $ vagrant up

to boot it again.

You can find out the state of a virtual machine anytime by invoking

    host $ vagrant status

Finally, to completely wipe the virtual machine from the disk **destroying all its contents**:

    host $ vagrant destroy # DANGER: all is gone

Please check the [Vagrant documentation](http://docs.vagrantup.com/v2/) for more information on Vagrant.


## Troubleshooting

On `vagrant up`, it's possible to get this error message:

```
The box 'ubuntu/yakkety64' could not be found or
could not be accessed in the remote catalog. If this is a private
box on HashiCorp's Atlas, please verify you're logged in via
vagrant login. Also, please double-check the name. The expanded
URL and error message are shown below:

URL: ["https://atlas.hashicorp.com/ubuntu/yakkety64"]
Error:
```

And a known work-around (https://github.com/Varying-Vagrant-Vagrants/VVV/issues/354) can be:

    sudo rm /opt/vagrant/embedded/bin/curl

