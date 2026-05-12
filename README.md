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
