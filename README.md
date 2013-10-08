# Intro to Vagrant

This document is meant to be a getting started guide to [Vagrant](http://vagrantup.com/). It will walk you 
through getting a development environment based on on the cwdg-base box setup on your computer, as well as point
out some common configuration problems.  Complete documentation about Vagrant can be found at http://vagrantup.com/.

## A note about the Terminal

When I talk about the Terminal throughout this document, I mean one of the following things:

If you're on Mac or Linux, I mean the Terminal.  Mac users, you can find the Terminal application in the Utilities folder (Go->Utilities). 
Linux people you know what the Terminal is.

If you're on Windows, the Terminal is Git Bash.  This is installed automatically for you when you install Git (outlined below).

## Base Boxes
If you know what you're doing, you're probably just looking for the base boxes, here they are:

* cwdg-base 64-bit https://dl.dropboxusercontent.com/u/7891705/cwdg-base.box
* cwdg-base 32-bit https://dl.dropboxusercontent.com/u/7891705/cwdg-base-32bit.box

You must make sure your processor's virtualization extensions are enabled in order to use the 64 bit box with VirtualBox.

## Installation

There are a few pieces of software that need to be installed prior to getting a development environment setup.

### Step 1: Install VirtualBox
Visit https://www.virtualbox.org/ to download the version of VirtualBox that works on your computer. It's an automatic installer, so hopefully nothing goes wrong.

### Step 2: Install Vagrant
Visit http://vagrantup.com/ to download and install the version of Vagrant for your system.  Once again it is a simple automatic installer.

### Step 3: Install Git
Visit http://git-scm.com/ and download the version of Git for your system.  There is an automated installer for this as well. The default options should work well enough.

If you're on something Unix like, you can install git through your package manager. I trust you're smart enough to figure out the package to install.

## Usage

Vagrant is a command line tool, and thus it helps to be familiar with Bash commands.  If you're new to bash don't worry, it isn't that bad, and it's 
a very useful thing to have a working knowledge of. Here is a good guide: http://mywiki.wooledge.org/BashGuide

### Importing the base box

Vagrant virtual machines are based on packaged VMs called boxes.  In order to create a new VM with Vagrant, you need a base box to start with. 
Base boxes can be thought of as templates for new VMs.  You maintain a local repository of base boxes from which you can create any number of individual 
VMs.  The <code>vagrant box</code> command is used to manage this local repository.

To start, we will add the cwdg-base base box to your computer's local box repository. You'll only have to do this once.

Type one of the following commands, depending on your system. If you want to use the 64-bit box, make sure the virtualization 
extensions are enabled on your computer.  You can enable them in the BIOS.  If you're not sure, go with the 32-bit box. 

For the 32-bit box, type at the terminal:
```
vagrant box add cwdg-base https://dl.dropboxusercontent.com/u/7891705/cwdg-base-32bit.box
```

For the 64-bit box, type at the terminal:
```
vagrant box add cwdg-base https://dl.dropboxusercontent.com/u/7891705/cwdg-base.box
```

This command will download the box from the given URL and add it to your local repository.  Once it is done type 
<code>vagrant box list</code> and verify that the cwdg-base box appears.

### Creating a new Virtual Machine

Now that the base box has been added to your repository, it is time to create a new virtual machine based off of it.

First, navigate to the directory you want to create the VM in.  For this example we will assume you want to use ~/cwdg as your workspace.
Type the following commands to change to this directory and create your first VM.

```
mkdir -p ~/cwdg
cd ~/cwdg
vagrant init cwdg-base
vagrant up
```

These commands do the following:

1. Make a new directory at ~/cwdg (~ is shorthand for your home directory).
2. Change the working directory to the newly created directory.
3. Add a Vagrantfile to the current directory that specifies the base box to use for our new VM.  In this case it is the cwdg-base box we imported earlier.
4. Start the virtual machine. Since this is the first time running the VM it will create it and then start it.

### SSH into the running VM

Once the <code>vagrant up</code> command finishes, it is time to SSH into your virtual machine.  Simply type 

```
vagrant ssh
```

And you will connect to your virtual machine.  You now have access to a Linux machine that is preconfigured with our Ruby on Rails development environment setup.

When you're done working in your VM, type <code>exit</code> to close the SSH connection and return to your computer's terminal, exactly how you would if you were
sshing into a remote server.

### Shutting down the VM

Just because you closed the SSH connection doesn't mean you're done.  The VM is still running in the background.  To shut it down, run:

```
vagrant halt
```

This will shutdown the VM.  Now you're done.

You can also use <code>vagrant reload</code> to restart the virtual machine.  This may be necessary after installing updates or making configuration changes in the Vagrantfile.


