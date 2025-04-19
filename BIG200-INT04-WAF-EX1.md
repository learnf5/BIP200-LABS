# Exercise 1 - Creating a Trust Relationship

## Requirements

Before you begin you need:

- A basic understanding of the Ansible client-less architecture

## Scenario

In this lab, you will learn how to build to Ansible trust relationships with a Linux server

## Objectives

At the end of this lab you will be able to:

- Invoke Ansible to perform a basic task on a remote host

## Lab

1. Test basic connectivity to a remote host

    Ansible is all about playbooks, but before you dive into them, look at the Ansible command line to better understand the Ansible environment

    1. The commands in the following steps must be entered in your home directory.  Type the following to change directory to your home directory and then confirm:

        **Note:** You must open a terminal window to perform the following tasks

        **Note:** Click on the icon to type the command into the terminal window
        
        **Note:** You must press RETURN to run the command

        `cd`

        `pwd`

        - "pwd" should display "/home/student"

    1. You must create an Ansible inventory file, which is a list of the machines you plan to configure or query. This file is typically named hosts, but should not be confused with the computer’s hosts file (/etc/hosts) which maps hostnames to IP addresses and is used when DNS is not available. So far, you only have one device to be work with, ubuntu1a:

        `nano ~/hosts`

        ```-linenums
        ubuntu1a
        ```

        **Note:** Don't forget to save the file in nano with a **CTRL-X** then **Y** then **RETURN**

    1. In the following step, Ansible is trying ping ubuntu1a to determine if it can configure it. Ansible attempts to ssh to ubuntu1a, but ssh is unable to connect because it is uncertain about the authenticity of the remote host. If you type yes, the connection will proceed. In this case, we want the command to complete without any further user intervention. Type **no** when you get to the prompt.

        **Synopsis:** ping is a trivial test module, that always returns pong on successful contact. It may not make sense in most playbooks, but it is useful to verify the ability to log in and confirm that Python is properly configured.  

        **Note:** This is not ICMP ping.

        - answer "no" when asked about conntinuing to connect

        `ansible ubuntu1a --inventory-file=hosts --module-name=ping`

        ```-nocopy
        The authenticity of host 'ubuntu1a (10.10.X.1)' can't be established.
        ECDSA key fingerprint is SHA256:dNFbvKxxCkb0g+3OGBxpYvgyAq21SGtf6/QsbhFqAqw.
        Are you sure you want to continue connecting (yes/no)? no
        ubuntu1a | UNREACHABLE! => {
            "changed": false, 
            "msg": "Failed to connect to the host via ssh: Host key verification fa... 
            "unreachable": true 
        }
        ```

        Type the following ssh command to confirm the first part of the Ansible message is from ssh:
        
        `ssh ubuntu1a`

        - answer "no" when asked about creating a fingerprint

        ```-nocopy
        The authenticity of host 'ubuntu1a (10.10.X.1)' can't be established.
        ECDSA key fingerprint is SHA256:dNFbvKxxCkb0g+3OGBxpYvgyAq21SGtf6/QsbhFqAqw.
        Are you sure you want to continue connecting (yes/no)?
        ```

        @lab.Activity(Question1)

    1. If you instinctively typed yes at either of the ssh prompts above, ubuntu1a is now in the known hosts file and you will need to remove it as shown here: 

        **Note:** Normally you would only delete the ubuntu1a entry within that file, but currently it is the only entry

        `rm ~/.ssh/known_hosts`

    1. To prevent the ssh warning, create an Ansible configuration file as shown here:

        `nano ~/.ansible.cfg`
        
        ```-linenums
        [defaults]
        host_key_checking=false
        ```

        **Note:** Don't forget to save the file in nano with a **CTRL-X** then **Y** then **RETURN**

        **Note:** Ansible allows you to override the default behavior of ansible commands using the following (in order of highest precedence):

        - **ANSIBLE_CONFIG**: Environment variable overrides individual user sessions

        - **ansible.cfg**: Overrides command launched from a specific directory

        - **~/.ansible.cfg**: Overrides commands launched by a specific user

        - **/etc/ansible/ansible.cfg**: Overrides any command launched on the host

        **Note:** Use a dot as the first character of the filename so you will be able to perform all the labs of this chapter. If you leave off the dot, the configuration options will only apply to ansible command run from this directory and you will need a configuration file for every other directory you use 

        **Note:** Starting a filename with a dot makes the file invisible to the base ls command. To see file names starting with a dot, use the command with a flag: `ls -a`

    1.	Try to run the ansible ping command again

        **Note:** Because of the above configuration, Ansible (using ssh) permanently added ubuntu1a to the list of known hosts. However, permission is still denied. Try ssh’ing as shown below and you will determine that ubuntu1a requires a password

        `ansible ubuntu1a --inventory-file=hosts --module-name=ping`

        ```-nocopy
        ubuntu1a | UNREACHABLE! => {
            "changed": false,  
            "msg": "Failed to connect to the host via ssh: Warning: Permanently added 'ubuntu1a,10.10.X.1' (ECDSA) to the list of known hosts.\r\nPermission denied (publickey,password).\r\n",  
            "unreachable": true 
        }
        ```

        `ssh ubuntu1a`

        - press CTRL-C at the password prompt

        ```-nocopy
        student@ubuntu1a's password:
        ```

    1.	Edit the hosts file to include the password for user student on ubuntu1a

        **Note:** The ~/hosts file aleady exists; in order to click-to-paste the new value, you need to delete the original file first

        `rm ~/hosts`
        
        `nano ~/hosts`

        **Note:** Spaces matter in the hosts file. Do not put spaces around the equal sign here

        ```-linenums
        ubuntu1a ansible_ssh_pass=student
        ```

    1.	Try the ansible command for a third time and note that it succeeds, but with a warning:

        `ansible ubuntu1a --inventory-file=hosts --module-name=ping`

        **Note:** Starting with Ansible 2.9, any system using Python 2 will generate a deprecation warning. You can get rid of the warning by telling Ansible to use Python 3 in the hosts file

        **Warning:** If you are using Ubuntu 18.04, you will receive the following warning:
[DEPRECATION WARNING]: Distribution Ubuntu 18.04 on host ubuntu1a should use /usr/bin/python3, but is using /usr/bin/python for backward compatibility with prior Ansible releases. A future Ansible release will default to using the discovered platform python for this host.

        See [https://docs.ansible.com/ansible/2.9/reference_appendices/interpreter_discovery.html] (https://docs.ansible.com/ansible/2.9/reference_appendices/interpreter_discovery.html) for more information. This feature will be removed in version 2.12. Deprecation warnings can be disabled by setting **deprecation_warnings=False** in ansible.cfg.

    1.	If you did not receive a deprecation warning, you should have seen the following output:

        ```-nocopy
        ubuntu1a | SUCCESS => {
            "ansible_facts": { 
                "discovered_interpreter_python": "/usr/bin/python3" 
            }, 
            "changed": false, 
            "ping": "pong" 
        }
        ```

    1.	Edit the .ansible.cfg file to include a directive to tell Ansible to use Python 3. Do not put spaces around the equal sign here:

        The **~/.ansible.cfg** file already exists -- delete it first if you are using the click-to-paste feature:

        `rm ~/.ansible.cfg`
        
        `nano ~/.ansible.cfg`

        ```-linenums
        [defaults]
        host_key_checking=false
        interpreter_python=python3
        ```

    1. Try the ansible command again and note that it succeeds this time without a warning or additional text. The command returns a success status and two additional lines:

        `ansible ubuntu1a --inventory-file=hosts --module-name=ping`

        ```-nocopy
        ubuntu1a | SUCCESS => {
            "changed": false,  
            "ping": "pong" 
        }
        ```

    1.	Answer the following questions:

        @lab.Activity(Question2)

        @lab.Activity(Question3)

        @lab.Activity(Question4)

        @lab.Activity(Question5)

        @lab.Activity(Question6)

1. Make the Ansible command more convenient to use

    1.	You can make the command a little shorter by avoiding the second argument if you add that information to the Ansible configuration file. Edit that information into the Ansible configuration you created earlier:

        **Note:** Spaces around the equal sign are acceptable in this file

        `rm ~/.ansible.cfg`
        
        `nano ~/.ansible.cfg`

        ```-linenums
        [defaults]
        host_key_checking=false
        interpreter_python=python3
        inventory=hosts
        ```

    1. Try the command now, without the inventory-file flag

        `ansible ubuntu1a --module-name=ping`

        ```-nocopy
        ubuntu1a | SUCCESS => {
            "changed": false,  
            "ping": "pong" 
        }
        ```

    1. Finally, if you want this command to apply to all of the hosts in the inventory, replace the host name with the word all

        **Note:** In your case there is only one host in that file, so the results will be the same

        `ansible all --module-name=ping`

        ```-nocopy
        ubuntu1a | SUCCESS => {
            "changed": false, 
            "ping": "pong" 
        }
        ```

        @lab.Activity(Question7)

    1. Edit the hosts file to include the username for user student on ubuntu1a

        **Note:** Spaces matter in the hosts file.  Do not put spaces around the equal sign here

        `rm ~/hosts`
        
        `nano ~/hosts`

        ```-linenums
        ubuntu1a ansible_ssh_user=student ansible_ssh_pass=student
        ```

    1.	Run the Ansible ping command again

        `ansible ubuntu1a --module-name=ping`

        @lab.Activity(Question8)

        @lab.Activity(Question9)
