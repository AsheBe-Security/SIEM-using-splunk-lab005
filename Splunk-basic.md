<img width="1168" height="663" alt="IMG_20260503_181858" src="https://github.com/user-attachments/assets/d27f0a97-b38b-45ab-94d7-54c0ca05c5f8" />

### SIEM lab designed using splunk

This lab is designed to centrally collect and organize logs from web server running using apache and windows logs which will be forwarded using splunk universalforwarder.
during this lab, i will undergoes 
#### Step one: fundamental installation and configuration 
  - Install splunk enterprise from www.splunk.com
      - Download locally and extract the zip file manually
      - Use CLI (recommended, prefrred tgz file)
          - wget -O splunk-10.2.3-4d61cf8a5c0c-windows-x64.msi "https://download.splunk.com/products/splunk/releases/10.2.3/windows/splunk-10.2.3-4d61cf8a5c0c-windows-x64.msi"
      - install splunk by extracting
          - tar -xzvf splunk-8.0.4.1-ab7a85abaa98-Linux-x86_64 -C /opt/
      - Creates use account for running splunk for better protection (avoid running it with root access)
          - sudo su (to move in to root access)
          - useradd -s /bin/bash -d /opt/splunk -m splunk
          - su - splunk (to move in to the user splunk)
          - /opt/splunk/bin/splunk start (to start splunk services)
          - Access the web interface by running the machine ip address together with the port 8000
                - 192.168.0.96:8000 (if it work, will take you to the splunk web interface)
      - configure splunk to recieve forwarded logs
          - Go to setting
          - forwarding and recieving
          - configure recieving
          - click New recieving port (would be 9997)
 - Install and run apache web service
        - sudo apt-get install apache2
        - sudo systemctl status apache2 (to check the status of apache2 service)
        - sudo systemctl restart apache2) (to restart the service)
        - open browser and type in the web server ip address, if it takes you the defualt apache web page, it works
 - Generate apache logs
      - First we need to locate the apache logs by moving in to
          - /var/log/apache2/
              - access.log
              - error.log
      - open the log file to see if logs are captured
           - sudo tail -f /var/log/apache2/access.log
           - sudo tail -f /var/log/apache2/error.log
      - Creates a log by accessing the apache web broswer we have lunched before
#### Step two splunk universal forwarder
  - Download splunk universal forwarder from splunk web (splunk.com)
        - wget -O splunkforwarder-10.2.3-4d61cf8a5c0c-linux-amd64.tgz "https://download.splunk.com/products/universalforwarder/releases/10.2.3/linux/splunkforwarder-10.2.3-4d61cf8a5c0c-linux-amd64.tgz"
  - extract the downloadable file using the command
      - tar -xzvf splunkforwarder-8.0.4-767223ac207f-Linux-x86_64.tgz -C /opt/
  -  Create user account for splunkforwarder
      -  useradd -s /bin/bash -d /opt/splunkforwarder -m splunk
  - Switch in to the splunk user to start the service
       - sudo su - splunk (moving in to the splunk user)
       - /opt/splunkforwarder/bin/splunk start (Starting the splunk forwarder service)
  - configure forwarder output (Telling the splunk forwarder where the splunk server lives)
      - sudo /opt/splunkforwarder/bin/splunk list forward-server (listing connected server)
      - sudo /opt/splunkforwarder/bin/splunk add forward-server IP:port
#### Step Three Configure Apache log monitoring
   - we need to check whether or not the two access files are add to forwader
       - sudo /opt/splunkforwarder/bin/splunk list monitor (listing the logs)
       - sudo /opt/splunkforwarder/bin/splunk add monitor /var/log/apache2/access.log
       - sudo /opt/splunkforwarder/bin/splunk add monitor /var/log/apache2/error.log
   - Restart the forwarder
       -/opt/splunkforwarder/bin/splunk restart
#### Step Four Verify log ingestion
   - on the splunk web interface
   - Got to search and report
   - your SPL = index=_internal or
   - source ="/var/log/apache2/access.log" or
   - host = apache-client name
#### Step Five Create a simple Dashboard
  - source ="/var/log/apache2/access.log"
  - Dashboard
  - Create new Dashboard
  - Give it a title
  - choose your charts and
  - file/event (type in the string like source=/vssr/log/apache2/access.log)
          
