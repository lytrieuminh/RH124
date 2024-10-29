#🤓 Guided Exercise: Gain Superuser Access
#🐱‍🚀🐱‍👤🐱‍💻🐱‍🐉🐱‍👓🐱‍🏍✨
[student@workstation ~]$ lab start users-superuser


1. From workstation, open an SSH session to servera as the student user.
[student@workstation ~]$ ssh student@servera

2. Explore the shell environment of the student user. View the current user and group information and display the current working directory. Also view the environment variables that specify the user's home directory and the locations of the user's executable files.
    2.1 Run id to view the current user and group information.
    [student@servera ~]$ id

    2.2 Run pwd to display the current working directory.
    [student@servera ~]$ pwd

    2.3 Print the values of the HOME and PATH variables to determine the home directory and user executables' path, respectively.
    [student@servera ~]$ echo $HOME
    [student@servera ~]$ echo $PATH

3. Switch to the root user in a non-login shell and explore the new shell environment.
    3.1 Run the sudo su command at the shell prompt to become the root user.
    [student@servera ~]$ sudo su
    [sudo] password for student: student
    [root@servera student]#

    3.2 Run id to view the current user and group information.
    [root@servera student]# id

    3.3 Run pwd to display the current working directory.
    [root@servera student]# pwd

    3.4 Print the values of the HOME and PATH variables to determine the home directory and user executables' path, respectively.
    [root@servera student]# echo $HOME
    /root
    [root@servera student]# echo $PATH
    /root/.local/bin:/root/bin:/sbin:/bin:/usr/sbin:/usr/bin:/usr/local/sbin:/usr/local/bin
    
    *** When you use the su command to become the root user, you do not keep the current path of the student user. As you can see in the next step, the path is not the root user path either.

    *** What happened? The difference is that you do not run su directly. Instead, you run the su command as the root user by using sudo because you do not have the password of the superuser. The sudo command overrides the PATH variable from the environment for security reasons. Any command that runs after the initial override can still update the PATH variable, as you can see in the following steps.

    3.5 Exit the root user's shell to return to the student user's shell.
    [root@servera student]# exit

4. Switch to the root user in a login shell and explore the new shell environment.
    4.1 Run the sudo su - command at the shell prompt to become the root user.

    The sudo command might or might not prompt you for the student password, depending on the time-out period of sudo. The default time-out period is five minutes. If you authenticated to sudo within the last five minutes, then the sudo command does not prompt you for the password. If more than five minutes elapsed since you authenticated to sudo, then you must enter student as the password for authentication to sudo.
    [student@servera ~]$ sudo su -
    [root@servera ~]#

    *** Notice the difference in the shell prompt compared to that of sudo su in the preceding step.

    4.2 Run id to view the current user and group information.
    [root@servera ~]# id

    4.3 Run pwd to display the current working directory.
    [root@servera ~]# pwd

    4.4 Print the values of the HOME and PATH variables to determine the home directory and the user executables' path, respectively.
    [root@servera ~]# echo $HOME
    /root
    [root@servera ~]# echo $PATH
    /root/.local/bin:/root/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin

    *** As in the preceding step, after the sudo command resets the PATH variable from the settings in the student user's shell environment, the su - command runs the shell login scripts for root and sets the PATH variable to yet another value. The su command without the dash (-) option does not have the same behavior.

    4.5 Exit the root user's shell to return to the student user's shell.
    [root@servera ~]# exit

5. Verify that the operator1 user can run any command as any user by using the sudo command.
[student@servera ~]$ sudo cat /etc/sudoers.d/operator1
operator1 ALL=(ALL) ALL

6. Become the operator1 user and view the contents of the /var/log/messages file. Copy the /etc/motd file to /etc/motdOLD. Remove the /etc/motdOLD file. As these operations require administrative rights, use the sudo command to run those commands as the superuser. Do not switch to root by using sudo su or sudo su -. Use redhat as the password of the operator1 user.
    6.1 Switch to the operator1 user.
    [student@servera ~]$ su - operator1
    Password: redhat
    [operator1@servera ~]$

    6.2 Try to view the last five lines of /var/log/messages without using sudo. It should fail.
    [operator1@servera ~]$ tail -5 /var/log/messages
    tail: cannot open '/var/log/messages' for reading: Permission denied

    6.3 Try to view the last five lines of /var/log/messages by using sudo. It should succeed.
    [operator1@servera ~]$ sudo tail -5 /var/log/messages
    [sudo] password for operator1: redhat

    6.4 Try to copy /etc/motd as /etc/motdOLD without using sudo. It should fail.
    [operator1@servera ~]$ cp /etc/motd /etc/motdOLD
    cp: cannot create regular file '/etc/motdOLD': Permission denied

    6.5 Try to copy /etc/motd as /etc/motdOLD by using sudo. It should succeed.
    [operator1@servera ~]$ sudo cp /etc/motd /etc/motdOLD
    [operator1@servera ~]$

    6.6 Try to delete /etc/motdOLD without using sudo. It should fail.
    [operator1@servera ~]$ rm /etc/motdOLD
    rm: remove write-protected regular empty file '/etc/motdOLD'? y
    rm: cannot remove '/etc/motdOLD': Permission denied

    6.7 Try to delete /etc/motdOLD by using sudo. It should succeed.
    [operator1@servera ~]$ sudo rm /etc/motdOLD

    6.8 Return to the workstation system as the student user.
    [operator1@servera ~]$ exit
    [student@servera ~]$ exit


✨ lab finish users-superuser
