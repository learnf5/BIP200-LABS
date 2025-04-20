@lab.Title

## Lab Contents

- [Exercise: Managing BIG-IP Next VE Instance in Central Manager](#exercise-managing-big-ip-next-ve-instance-in-central-manager)

- [Exercise: Licensing BIG-IP Next VE Instance](#exercise-licensing-big-ip-next-ve-instance)

- [Exercise: Deploying a Basic Application using Central Manager](#exercise-deploying-a-basic-application-using-central-manager)

- [Exercise: Migrating Application from Version 17.1 to BIG-IP Next](#exercise-migrating-application-from-version-17-1-to-big-ip-next)

## Lab Credentials and IP Address List

| External IP  | Internal IP   | Management IP  | Name          | Credentials / Comments |
|--------------|---------------|----------------|---------------|------------------------|
| 10.10.0.0/16 | 172.16.0.0/16 | 192.168.0.0/16 |               | *Lab Network*          |
| 10.10.0.254  |               | 192.168.0.254  |               | *Default Route*        |
| 10.10.1.30   |               | 192.168.1.30   | jump          | **student / student**  |
| 10.10.1.31   | 172.16.1.31   | 192.168.1.31   | bigip1        | **admin / F5trn001!**  |
| 10.10.1.32   | 172.16.1.32   | 192.168.1.32   | bigip2        | **admin / F5trn001!**  |
|              |               | 192.168.1.51   | cm1           | **admin / F5trn001!**  |
| 10.10.1.102  |               |                | juice-shop-vs | *Virtual Server*       |
|              | 172.16.20.160 |                | juice-shop    | *Backend Server*       |

## Lab Topology

!IMAGE[ht8ne4c7.jpg](instructions261554/ht8ne4c7.jpg)

<!--
## Click-to-Paste Shortcuts !!! Remove this section

In the following lab steps, you will be instructed to create various files.  You can use the available click-to-paste shortcuts on the next pages to avoid creating these new files by hand.  In general, this is not recommended because it is beneficial to manually add these files.  You will become more familiar with the individual directives as well as the overall syntax.  Making mistakes in the lab will lead to troubleshooting that further increases understanding and familiarity.

However, it is acknowledged that some students have poor typing skills and that spending time typing and retyping commands and directivies can be very frustrating.  For these students, shortcuts are available that bypass all the typing and perform the specific action described in the student lab guide.

**TL;DR:** In the following lab steps, you will have the option to create files and run commands manually, or you can choose click-to-paste shortcuts.  Don't choose the shortcuts.
-->
