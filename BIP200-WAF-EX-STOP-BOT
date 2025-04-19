# Exercise: Stopping Talking to Bots

[Return to Lab Contents](#lab-contents)

## Requirements

Before you begin, you need

- A BIG-IP Next instance 

- An application security policy applied to the BIG-IP Next instance

## Scenario

In this lab, you will send requests from Apache Bench and review handling of bot traffic.

## Objectives

At the end of this lab you will be able to:

- Understand and apply bot mitigation options as desired

- Locate bot activity in the event request log

## Lab

### A. Review bot mitigation options in the application security policy

1. In BIG-IP Next Central Manager, navigate to **SECURITY >> WAF > Policies**

1. On the resulting **Policies** page click your policy (The name is a link.)

1. In the **WEB PROTECTION** section on the left select **Bot Protection** near the bottom of the list.

1. Review the **Mitigations Settings** for each bot category. Make note of the action taken on **Untrusted Bot** and **Malicious Bot** so that you can trigger an associated violation and then modify the mitigation setting.

1. Click **Cancel** at the bottom left to return to the Security page.

### B. Send a request from a bot

1. Open a terminal window and run the following command from Apache Bench:
`ab -k -c 1 -n 5 http://10.10.1.102/ `

    - The command sends 5 simultaneous connections, with Keep-Alive header, until 5 requests are met.

### C. Review the WAF Dashboard

1.  In BIG-IP Next Central Manager, navigate to **SECURITY >> Monitoring > WAF Dashboard**

1. Take a moment to review the dashboard. You should see several blocked requests. Refresh the page if you do not see any blocked requests.

1. Scroll to the bottom right of the dashboard and locate the **Bot Signatures (Top 20)** section. You should see the **ab** signature triggered by your Apache Bench request. Click anywhere in the row to review more data.
