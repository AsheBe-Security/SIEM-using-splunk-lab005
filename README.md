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
#### Step two splunk universal forwarder
          
    - analyzing logs forwarded from both apache and windows
    -simulate brutforce attack and detect it using splunk and take leason from it
    - failed login /authentication attack on windows 
