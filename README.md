<img width="1168" height="663" alt="IMG_20260503_181858" src="https://github.com/user-attachments/assets/d27f0a97-b38b-45ab-94d7-54c0ca05c5f8" />

### SIEM lab designed using splunk

This lab is designed to centrally collect and organize logs from web server running using apache and windows logs which will be forwarded using splunk universalforwarder.
during this lab, Three Task were carried out

### Task 1 Basic task
**fundamental installation and configuration** 
  - Install splunk enterprise (www.splunk.com)
      - Download and install splunk 
      - Creates user account for running splunk for better protection (avoid running it with root access)
      - configure splunk to recieve forwarded logs
 - Install and run apache web service
        -To create web server, we need to download apache and run it on your vm
 - install and run splunk universal forwarder on apache machine
 - configure apache logs on splunk fowarder
    - This was achieved by locating both the access.log and error.log on apache and add these log files in to the forwarder monitor
    - neccessary test was carried out on every step of the way
### Task 2 Brute force attack detection 
i have used ssh service for simulating a brute force attack
  - i have install and run ssh service from openssh-server
  - check if there is auth.log on apache server to see successful or failed login attempts
  - by accessing the splunk web inteface we provide the path to auth.log in to Directories
  - provided index under the name ssh_logs so that any data can easily be located within this index
  - for the first time we provided the right credentials to see how the logs behave and on the second time, i used wrong login too many time. Logs with failed login was created from one single ip address.
