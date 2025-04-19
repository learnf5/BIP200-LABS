# Exercise 2 - Creating an Alternate Trust Relationship

## Requirements

Before you begin you need to understand:

- How to use a simple Ansible command with the same local and remote username

## Objectives

At the end of this lab you will be able to:

- How to use a simple Ansible command with different local and remote usernames

## Lab

1. Ping a remote host with an alternate username

    1. Edit the hosts file to include both the new username and new password for the remote user

        **Note:** You must open a terminal window to perform the following tasks

        **Note:** Click on the icon to type the command into the terminal window
        
        **Note:** You must press RETURN to run the command

        **Note:** The ~/hosts file aleady exists; in order to click-to-paste the new value, you need to delete the original file first

        `rm ~/hosts`
        
        `nano ~/hosts`

        ```-linenums
        ubuntu1a ansible_ssh_user=ansible ansible_ssh_pass=ansible
        ```

        **Note:** Don't forget to save the file in nano with a **CTRL-X** then **Y** then **RETURN**

    1.	Rerun the Ansible ping command

        `ansible all --module-name=ping`

        ```-nocopy
        ubuntu1a | SUCCESS => {
            "changed": false, 
            "ping": "pong" 
        }
        ```

       @lab.Activity(Question10) 

        Note: In the ansible command above, you changed the target from ubuntu1a to all, which runs the command on every computer in the hosts file (but there is only one, so far)

1. Run a different command

    1. Until now, you have only used the ping module in the ansible command.   Try a new one here:

        `ansible all --module-name=command --args=date`

        ```-nocopy
        ubuntu1a | SUCCESS | rc=0 >>
        Sun Mar 18 21:50:40 EDT 2018
        ```

    1. Answer the following questions:

        @lab.Activity(Question11)

        @lab.Activity(Question12)

1. Run a command that requires superuser privileges

    1. Use ansible to run the apt update command as shown here:

        `ansible all --module-name=apt --args="update-cache=true"`

        ```-nocopy
        ubuntu1a | FAILED! => {
            "changed": false,  
            "msg": "Failed to lock apt for exclusive operation" 
        }
        ```

        @lab.Activity(Question13)

        @lab.Activity(Question14)

        @lab.Activity(Question15)

    1. The **apt update** command needs to run as superuser (root). Change the username and password in the hosts file to root as shown here:

        `rm ~/hosts`
        
        `nano ~/hosts`

        ```-linenums
        ubuntu1a ansible_ssh_user=root ansible_ssh_pass=root
        ```

    1. Rerun the Ansible command

        `ansible all --module-name=apt --args="update-cache=true"`

        ```-nocopy
        ubuntu1a | UNREACHABLE! => {
            "changed": false,  
            "msg": "Authentication failure.",  
            "unreachable": true 
        }
        ```

    1.	Answer the following question:

        @lab.Activity(Question16)

    1. Test it for yourself by ssh’ing to ubuntu1a as root

        `ssh root@ubuntu1a`

        - Enter `root` as the password

        ```-nocopy
        root@ubuntu1a's password: root
        Permission denied...Authentication failed
        ```

        @lab.Activity(Question17)

        **Hint:** the ssh results give you the answer

    1. You tried using Ansible to log in as user ansible and discovered you did not have sufficient privileges.  Next you tried logging in as root only to learn that didn’t work either because Ubuntu will not allow ssh to the superuser (root) account.  Try using Ansible to log in with a working, non-privileged account and escalate privileges with sudo.  Edit the hosts file as shown

        **Remember:** With sudo, you use the user’s password, not the root password 

        **Note:** This line has gotten very long and has wrapped around twice as shown below, but this is all one line in the file. If you insert it into the file as three lines, the command will fail

        `rm ~/hosts`
        
        `nano ~/hosts`
        
        ```-linenums
        ubuntu1a ansible_ssh_user=ansible ansible_ssh_pass=ansible ansible_become=true ansible_become_method=sudo ansible_sudo_pass=ansible
        ```

    1. In addition to the hostname, there are five directives on this line. This is what each of them does:

        Directive                  | Role
        ---------------------------|---------------------------------------------------------------------
        ansible_ssh_user=ansible   | Ssh login username for remote device
        ansible_ssh_pass=ansible   | Ssh login password for remote device
        ansible_become=true        | After login, become superuser
        ansible_become_method=sudo | After login, become superuser using the sudo command
        ansible_sudo_pass=ansible  | Password to use at the sudo prompt (i.e., the user's login password)

    1. Rerun the Ansible command to perform an apt update

        `ansible all --module-name=apt --args="update-cache=true"`

        ```-nocopy
        ubuntu1a | SUCCESS => {
            "cache_update_time": 1521425072,  
            "cache_updated": true,  
            "changed": true 
        }
        ```

        @lab.Activity(Question18)

        @lab.Activity(Question19)

1. Use su instead of sudo

    1. On some machines, sudo may not be available, or the user account may not have sudo access.  In this case, you will need to use the su method to escalate privilege mode, ie, become superuser.  Test the following example:

        - Save the old hosts file to compare against the new one in the next step
        
        `mv ~/hosts ~/hosts.old`
        
        `nano ~/hosts`
        
        ```-linenums
        ubuntu1a ansible_ssh_user=ansible ansible_ssh_pass=ansible ansible_become=true ansible_become_method=su ansible_su_pass=root
        ```

    1. Two of the directives changed this time.  What are the two directives that changed?  List the old and new hosts files to review the differences:

        `cat ~/hosts.old ~/hosts`

        @lab.Activity(Question20)

        @lab.Activity(Question21)

        **Note:** If you don’t change the second directive, the ansible command will fail with a Timeout waiting for privilege escalation prompt message

    1. Rerun the Ansible command

        `ansible ubuntu1a --module-name=apt --args="update-cache=true"`

        @lab.Activity(Question22)

        @lab.Activity(Question23)

        @lab.Activity(Question24)
