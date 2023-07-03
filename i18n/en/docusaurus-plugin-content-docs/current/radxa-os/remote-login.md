---
sidebar_label: 'Remote Login'
sidebar_position: 60
---

# Remote login

## SSH

This is a tutorial on how to log in to ROCK 5A remotely using SSH from a Windows computer.  

To connect to a Debian system via the SSH protocol, you need to make sure that an SSH server is installed on the Debian system. You can do this by following these steps:   

1. Make sure that an SSH server is installed on the Debian system. Run the following command in a terminal: 

    sudo service ssh status
If the SSH server is not installed, you can use the following command to install it:

    sudo apt-get update
    sudo apt-get install ssh

2. Open the terminal program and enter the following command: 

    ssh [username]@[hostname]
    or  
    ssh [username]@[IP address]  
Example: 

    ssh radxa@192.168.1.100

3. You need to enter the user password to successfully connect to the Debian system.
This is a basic SSH connection process. You can use other SSH options for more advanced connections.


## Remote Desktop - KDE Desktop

This is a tutorial on how to access your system remotely from a Windows computer using VNC.  

### Installing VNC Server

1. Open the Terminal application and enter the following command to update the package list.   

```
sudo apt-get update
```

2. Enter the following command to install tightvncserver.  

```
sudo apt install tigervnc-standale-server
```
3. Install the dbus-x11 dependencies to ensure proper connection to your VNC server: 
```
sudo apt install dbus-x11
```
4. After installation complete the initial configuration of the VNC server, use the vncserver command to set the security password and create the initial configuration file: ``budo apt install dbus-x11  

```
vncserver
```

    Next you will be prompted to enter and verify a password for remote access to your device: 
        You will require a password to access your desktops.
        Password.
        Verify.
    
    The length of the password must be between six and eight characters. Passwords longer than eight characters will be automatically truncated.
    Once you have verified the password, you have the option to create a view-only password. Users who log in with a view-only password will not be able to control the VNC instance with the mouse or keyboard.
    This is a useful option if you want to demonstrate something to other people using the VNC server, but it is not required.
        You will require a password to access your desktops.
        Password.
        Verify.
        Would you like to enter a view-only password (y/n)? n
    
        New 'X' desktop is rock-5b:1
    
        Creating default startup script /home/radxa/.vnc/xstartup
        Starting applications specified in /home/radxa/.vnc/xstartup
        Log file is /home/radxa/.vnc/rock-5b:1.log
    


### Configure the VNC server

1. Once tightvncserver starts, it will create a VNC session with the IP address and port number of the VNC server (usually 5901), because to change the way the VNC server is configured, first stop the VNC server instance running on port 5901 with the following command:
```
vncserver -kill :1
```
   When VNC is first set up, it starts a default server instance on port 5901. This port is called the display port and is referred to by VNC as :1. VNC can start multiple instances on other display ports, such as :2, :3, etc.

2. Running the vncserver command will generate an xstartup in the ~/.vnc directory. If it is not generated, please create it manually and grant executable permissions:
```
touch ~/.vnc/xstartup
chmod +x ~/.vnc/xstartup
```
Edit the xstartup configuration file as follows:
```
radxa@rock-5b:~$ cat ~/.vnc/xstartup
#! /bin/sh
unset SESSION_MANAGER
unset DBUS_SESSION_BUS_ADDRESS
unset XDG_RUNTIME_DIR
/etc/X11/xinit/xinitrc
[ -x /etc/vnc/xstartup ] && exec /etc/vnc/xstartup
[ -r $HOME/.Xresources ] && xrdb $HOME/.Xresources
xsetroot -solid grey
#vncconfig -iconic &
startkde &
```
3. After the configuration is edited, restart the VNC server:
```
vncserver -localhost no
```
4. View the VNC server:
```
vncserver -list
TigerVNC server sessions.
X DISPLAY # RFB PORT # PROCESS ID SERVER
:1 5901 2160 Xtigervnc
:2 5902 2872 Xtigervnc
```
5. Test the connection on the VNC viewer: On your Windows PC, open the VNC viewer, enter the IP address and port number of your product, and then authenticate using the user name and password of the VNC server.    

### Installing the VNC viewer on your Windows PC

1. Go to the VNC Viewer download page on your web browser, e.g. https://www.realvnc.com/en/connect/download/viewer/  
2. Download and install the VNC viewer. 

### Connection setup

1. On the VNC viewer, enter the IP address and port number of the product. 2.  
2. Use the user name and password of the VNC server to authenticate. 3.
3. After successful connection, you can control remotely. 
