# Connect to Ubuntu from Windows using RDP :
  
  - Open a terminal in Ubuntu 18.0 LTS and write these commands.
    ```
    sudo apt-get update
    sudo apt-get install xrdp
    sudo apt-get install xfce4
    sudo apt-get install xfce4
    sudo nano /etc/xrdp/startwm.sh | (Remove the line . /etc/X11/Xsession and add the line startxfce4 and then hit ctrl+X and save the file.)
    sudo service xrdp restart
    ```
  - Now in Windows 10 Launch the RDP client (Remote Desktop Connection) on Windows machine and Connect to the IP address of Ubuntu Machine.To scale resolution and others Click Advance on Remote Desktop Connection and set your desired settings. Set Bandwidth to Broadband 2-10 MBPS to get good speed.
     
      
# Zip a file 
  ```
  sudo apt-get install zip
  zip -r example.zip original_folder [Here example.zip will be the zipped file while “original_folder” is the main file]
  ```
  
# Download a file using HFS
  ```
  curl http://IP:PORT/FILE.EXT --output yourFile.txt
  ```
      
# Send file by Python Server.

  - First zip a file. 
  - Now write these commands.
    ```
    sudo fuser -k 8000/tcp
    cd /folder/to/share
    python -m SimpleHTTPServer
    ```

# Find all open ports
  ```
  sudo ufw status
  sudo ufw allow 80/tcp [open a specific port]
  sudo ufw deny 80/tcp [close a specific port]
  sudo ufw delete deny 80/tcp [delete a role]
  ```







