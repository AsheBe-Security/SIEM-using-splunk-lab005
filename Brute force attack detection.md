## Lab 005 Brute force attack using ssh service on splunk
objectives: by the end of this lab, i will be able to
    - run ssh service on both the attack and victim machine running on vm
    - install and configure splunk enterprise on ubuntu 
    - install anf configure splunk universal forwarder on the attack machine to see of log can be generated on splunk
    - creates both failed login and successful login on the ssh service to see how logs behaves 
    - filtters collected logs using different spl (search key words) and use these filters to creates both dashboard and alerts 

Architecture of this lab 
    = Ubuntu os - running splunk server - ip = 192.168.0.77
    = Kali linux - running universal forwarder & ssh service - ip = 192.168.0.78
Steps used on this lab 
1. Download andd install important packages
       - Look basic SEIM pages for detials on how to donwnload and install both
                 - splunk enterprise
                 - splunk universal forwarder
2. Configuration of both splunk and universal forwarder
       - For running and configuring splunk to recieve forwarding logs, see splunk basic pages on this lab
       - For splunk universal forwarder, we need to find the right logs to add it in to the monitor on splunk forwarder
       - Because, we can't find auth.log on kali we need to download rsyslog
                  - sudo apt install rsyslog -y
       - Check if the log file exists
                  - cd /var/log
       - checl if logs is being captures on the auth.log, by sending ssh request from the victim machine to the attacker and open the log file
                  - sudo tail -f auth/log (sudo tail -f /var/log/auth.log
