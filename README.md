# redis-win10-wsl-install-guide


Steps to install latest version of redix on Win (WSL): 

At present (15/04/20), this is the only way to run the latest version of redix.\
The current redis version is 5.0.8. \
Some older versions that runs on windows are available at:\
https://github.com/dmajkic/redis/downloads \
https://github.com/ServiceStack/redis-windows/tree/master/downloads 

But they are a few major patches behind (2.x, 3.x) so I figured I should stick with the latest.

**1 - Open PowerShell as Administrator and run:**

*Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux*

**2- Restart PC when prompted**

**3 - Choose a linux distro** 

https://docs.microsoft.com/en-us/windows/wsl/install-manual \
I chose the debian distro because it is the most stable one (google search)

**4 - Open PowerShell as Administrator in the folder with the .appx file and run:**

*Add-AppxPackage .\app_name.appx*\
where app_name is the name of the linux distro. Ex:\
*Add-AppxPackage .\DebianGNULinux_1-1-3-0_x64__76v4gfsz19hv4.appx*\
A shortcut to open PowerShell as Administrator in that folder => \
"Shift" + right-click on an empty space to get the context menu with the option Run PowerShell as Administrator in that folder.

**5 - After it is installed open it from the start menu**

**6 - Create a unix username** (a-z A-Z .  _ -) Don't start with hyphen - 

**7 - Create a unix password** 

  > Minimum of 8 characters.\
  > Cannot be dictionary words, your name, your account name, or common strings.\
  > Use at least 3 of 4 character sets: uppercase, lowercase, numerals, symbols.\
  >  Do not use spaces in your password.  
  
I think this is the standard for a unix password. A confirm message asking to re-enter the password will appear when it accepts the password we entered.

**8 - After being logged in, the instructions on https://redis.io/topics/quickstart are to enter the following commands:**

*wget http://download.redis.io/redis-stable.tar.gz* \
*tar xvzf redis-stable.tar.gz*\
*cd redis-stable*\
*make*

Except bash will complain about not having a *make* command\
Running the following lines will install *make*. I guess they are used to initialize linux (I don't know the first thing about linux)\
*sudo apt-get update*\
*sudo apt-get install build-essential*

Then run:

*wget http://download.redis.io/redis-stable.tar.gz* \
*tar xvzf redis-stable.tar.gz*\
*cd redis-stable*\
*make*

"make" will take a few minutes to execute.

**9 - Run:**\
    *sudo cp src/redis-server /usr/local/bin/*
    *sudo cp src/redis-cli /usr/local/bin/*\
	**OR**
	sudo make install
	
On https://github.com/ServiceStack/redis-windows 
they said "Installing the binaries using make install will not work. You need to copy them manually to /usr/bin (just like described in the guide, except that they use /usr/local/bin - which is the problem" 
Maybe not then but now it works fine without this workaround.

**10 - Run:**

*redis-server* \
This starts the redis server connection

**11 - Open another linux bash and run:**

*redis-cli*\
It will print:\
*127.0.0.1:6379>*\
Test it by running "ping"
It will return "PONG"

That's it! 

To edit the config file you can run *sudo nano redis.conf*\
**update: Just learnt about remote - wsl extension in vs code that let you "Open any folder in the Windows Subsystem for Linux (WSL) and take advantage of Visual Studio Code's full feature set."**

Ctrl + C to stop redis-server and redis-cli

Anyway, that's how I got it working. If I made any mistakes, please correct me. 
