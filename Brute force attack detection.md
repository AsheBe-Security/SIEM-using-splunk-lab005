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
     - check if logs is being captures on the auth.log, by sending ssh request from the victim machine to the attacker and open the log file
          - sudo tail -f auth/log (sudo tail -f /var/log/auth.log)
          - check the last logs (the date, the ip address, the service requested and login (successful or failed))
     - Add the splunk server ip address and the port number to send longs to slunk (logs ingustion)
          - sudo /opt/splunkforwarder/bin/splunk add forwarder-server ip-address:ports(9997)
     - provide this log file path in to splunk forwarder for splunk to collect logs from that machine
          - sudo /opt/splunkforwarder/bin/splunk add monitor /var/log/auth/log
          - sudo /opt/splunkforwarder/bin/splunk list monitor (_to check whether the log files with its path have been added in to forwarding_)
          - on the splunk web page, go to data input and provide the detials -  index = main, sourcetype = linux_secure
3. Check if log ingestion is successful on splunk server
          - First, we need to restart splunk universal forwarder
               - sudo /opt/splunkforwarder/bin/splunk restart
          - Go to splunk web pages and under app click search and report and type in the following spl
               - index=main sourcetype=linux_secure "Failed password" OR "Accepted password"
