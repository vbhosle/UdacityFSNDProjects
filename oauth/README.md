# OAuth2.0
Part of Auth&amp;Auth course

# If you don't want to install VM, make sure that following installations are available on your machine
`apt-get -qqy install python3 python3-pip
pip3 install --upgrade pip
pip3 install flask packaging oauth2client redis passlib flask-httpauth
pip3 install sqlalchemy flask-sqlalchemy psycopg2 bleach requests`

# Installing the Vagrant VM for ud330 - Authentication & Authorization

**Note: If you already have a vagrant machine installed from previous Udacity courses skip to the 'Fetch the Source Code and VM Configuration' section**

In Lessons 2,3 and 4 of this course, you'll use a virtual machine (VM) to run a web server and a web app that uses it. The VM is a Linux system that runs on top of your own machine.  You can share files easily between your computer and the VM.

We're using the Vagrant software to configure and manage the VM. Here are the tools you'll need to install to get it running:

### Git

If you don't already have Git installed, [download Git from git-scm.com.](http://git-scm.com/downloads) Install the version for your operating system.

On Windows, Git will provide you with a Unix-style terminal and shell (Git Bash).  
(On Mac or Linux systems you can use the regular terminal program.)

You will need Git to install the configuration for the VM. If you'd like to learn more about Git, [take a look at our course about Git and Github](http://www.udacity.com/course/ud775).

### VirtualBox

VirtualBox is the software that actually runs the VM. [You can download it from virtualbox.org, here.](https://www.virtualbox.org/wiki/Downloads)  Install the *platform package* for your operating system.  You do not need the extension pack or the SDK. You do not need to launch VirtualBox after installing it.

**Ubuntu 14.04 Note:** If you are running Ubuntu 14.04, install VirtualBox using the Ubuntu Software Center, not the virtualbox.org web site. Due to a [reported bug](http://ubuntuforums.org/showthread.php?t=2227131), installing VirtualBox from the site may uninstall other software you need.

### Vagrant

Vagrant is the software that configures the VM and lets you share files between your host computer and the VM's filesystem.  [You can download it from vagrantup.com.](https://www.vagrantup.com/downloads) Install the version for your operating system.

**Windows Note:** The Installer may ask you to grant network permissions to Vagrant or make a firewall exception. Be sure to allow this.

## Fetch the Source Code and VM Configuration

**Windows:** Use the Git Bash program (installed with Git) to get a Unix-style terminal.  
**Other systems:** Use your favorite terminal program.

From the terminal, run:

    git clone https://github.com/udacity/OAuth2.0 oauth

This will give you a directory named **oauth** complete with the source code for the flask application, a vagrantfile, and a bootstrap.sh file for installing all of the necessary tools.

## Run the virtual machine!

Using the terminal, change directory to oauth (**cd oauth**), then type **vagrant up** to launch your virtual machine.

# Obtain OAuth credentials for Google
Sign in to https://console.developers.google.com/
Goto API & Services>credentials>Create credentials
Select OauthCLIENTID> Application Type: "Web Application"
Enter following details:
1. Name of the application
2. Authorized Javascript origins (http://localhost:5000)
and click Create
Now under the application name, you can click 'DOWNLOAD JSON', which includes
3. client_id
4. project_id
5. client_secret
**Save json as client_secrets.json' in project's root directory**
**NOTE: Never share client secret with anyone and never upload it on repo**

# Obtain OAuth credentials for Facebook
Create account at https://developers.facebook.com/ and login into it.
Under My Apps on top right, select **Add new app**
Provide display name (i.e app name) and email id
That will give you
6. APP_ID
7. APP_SECRET

# Replace credentials for OAuth2

In **client-secrets.json**, update PUT_YOUR_CLIENT_ID(obtained at 1), PUT_YOUR_APPLICATION_NAME(3), PUT_YOUR_CLIENT_SECRET(4) or replace this json with downloaded json from Google.

In **templates/login.html**, update CLIENT_ID(1), FACEBOOK_APP_ID(6)

In **fb_client_secrets.json**, update YOUR_APP_ID(6), YOUR_APP_SECRET(7)

## Running the Restaurant Menu App with oauth
Once it is up and running, type **vagrant ssh**. This will log your terminal into the virtual machine, and you'll get a Linux shell prompt. When you want to log out, type **exit** at the shell prompt.  To turn the virtual machine off (without deleting anything), type **vagrant halt**. If you do this, you'll need to run **vagrant up** again before you can log into it.


Now that you have Vagrant up and running type **vagrant ssh** to log into your VM.  change to the /vagrant/oauth directory by typing **cd /vagrant/oauth**. This will take you to the shared folder between your virtual machine and host machine.

Type **ls** to ensure that you are inside the directory that contains project.py, database_setup.py, and two directories named 'templates' and 'static'

Now type **python database_setup.py** to initialize the database.

Type **python lotsofmenus.py** to populate the database with restaurants and menu items. (Optional)

Type **python project.py** to run the Flask web server. In your browser visit **http://localhost:5000** to view the restaurant menu app.  You should be able to view, add, edit, and delete menu items and restaurants.