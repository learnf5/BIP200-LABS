## Lab Contents

- Lab 3: Creating a Trust Relationship

- Lab 4: Creating an Alternate Trust Relationship

## Lab Credentials and IP Address List

External IP  | Internal IP   | Management IP | Hostname | Credentials / Comments
-------------|---------------|---------------|----------|-----------------------------------
10.10.0.0/16 | 172.16.0.0/16 | 192.168.0.0   |          | *Lab Network*
10.10.0.33   |               | 192.168.0.33  |          | *Default Route*
10.10.1.1    |               |               | ubuntu1a | **student / student**
10.10.1.2    |               |               | ubuntu1b | **student / student**
10.10.1.29   |               | 192.168.0.29  | jump1    | **student / student**
10.10.1.31   | 172.16.1.31   | 192.168.1.31  | bigip1a  | **admin\|root / f5trn001**
10.10.1.32   | 172.16.1.32   | 192.168.1.32  | bigip1b  | **admin\|root / f5trn001**
10.10.1.33   | 172.16.1.33   |               |          | *HA Self-IP*
10.10.1.101  |               |               | app1     | *Virtual Server*
10.10.1.101  |               |               | wiki1    | *Virtual Server*
10.10.1.101  |               |               | www1     | *Virtual Server*

## Lab Network Topology

!IMAGE[0u9e19nj.jpg](instructions247483/0u9e19nj.jpg)

## Click-to-Paste Shortcuts

In the following lab steps, you will be instructed to create various files.  You can use the available click-to-paste shortcuts on the next pages to avoid creating these new files by hand.  In general, this is not recommended because it is beneficial to manually add these files.  You will become more familiar with the individual directives as well as the overall syntax.  Making mistakes in the lab will lead to troubleshooting that further increases understanding and familiarity.

However, it is acknowledged that some students have poor typing skills and that spending time typing and retyping commands and directivies can be very frustrating.  For these students, shortcuts are available that bypass all the typing and perform the specific action described in the student lab guide.

**TL;DR:** In the following lab steps, you will have the option to create files and run commands manually, or you can choose click-to-paste shortcuts.  Don't choose the shortcuts.
