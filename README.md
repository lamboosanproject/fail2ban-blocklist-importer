fail2ban-blocklist-importer
===========================

A small script to import and ban IPs from a list (like from blocklist.de). The list has to be formatted one IP per line, with no additional text.

After fetching the list, the script will add each IP to fail2bans blocklist jail and trigger the actual banning by touching the appropiate log file.

* Tested on:
    *   Ubuntu 22.04 Jammy
    *   SystemD          - 249.11-0ubuntu3.12
    *   fail2ban         - 0.11.2-6
    *   python3          - 3.10.6-1~22.04
    *   python3-requests - 2.25.1+dfsg-2ubuntu0.1

Configuration
-------------
Copy folder with config file 
*   **cp -r etc/fail2ban-importer /etc/fail2ban-importer**
*   **mkdir /var/log/fail2ban/**

In the script, edit the config file:
*   **socket:** The socket used by fail2ban
*   **url:** The URL of the list.
*   **jail type:** Contains information about the type of jail block.
*   **logfile:** Full path of the Logfile used in the Jail configuration. This file will be crated if it does not exist.
*   **loglevel:** How much should be logged. Currently used values are: logging.DEBUG, logging.INFO, logging.ERROR

In system copy systemd unit files (in project etc/systemd/system) to etc/systemd/system/ and run 
*   **systemctl daemon-reload**
*   **systemctl enable fail2ban-blockip-importer-timer.timer**
*   **systemctl restart fail2ban-blockip-importer-timer.timer**

Then check status service.

> *If your fail2ban modules are not in `/usr/share/fail2ban`, you need to change the import on line 11 according to your needs.*

TODO
----

*   Get Socket and Logfile Configuration from fail2ban
*   handle unblocking of IPs

Credit
------

This script was inspired by [Kapsonfile](https://forum.blocklist.de/viewtopic.php?f=11&t=107#p333 "Thank you!")

Modified for SystemD and python3.10+ [Victor "LambooSan" Horovyi]()
