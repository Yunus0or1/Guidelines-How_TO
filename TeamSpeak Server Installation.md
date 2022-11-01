# TeamSpeak Server Installation

 - First download Linux 64 bit server from [here](https://www.teamspeak.com/en/downloads/#server).
 - Copy it to Desktop. Extract it. Rename it as teamspeak.
 - Open a terminal inside the **teamspeak** folder and type these commands.
   ```
   sudo touch /home/<user>/Desktop/teamspeak/.ts3server_license_accepted
   sudo nano /lib/systemd/system/teamspeak.service
   ```

 - Copy these lines into teamspeak.service file.
   ```
   [Unit]
   Description=TeamSpeak 3 Server
   After=network.target
   [Service]
   WorkingDirectory=/home/<user>/Desktop/teamspeak/
   User=<user>
   Group=<usergroup. it should be like your User>
   Type=forking
   ExecStart=/home/<user>/Desktop/teamspeak/ts3server_startscript.sh start inifile=ts3server.ini
   ExecStop=/home/<user>/Desktop/teamspeak/ts3server_startscript.sh stop
   PIDFile=/home/<user>/Desktop/teamspeak/ts3server.pid
   RestartSec=15
   Restart=always
   [Install]
   WantedBy=multi-user.target
   ```
   Press CTRL+X -> Y -> Enter
 - Now write these commands.
   ```
   sudo systemctl enable teamspeak.service
   sudo systemctl start teamspeak.service
   ```
 - Check if running.
   ```
   sudo systemctl status teamspeak
   ```
 - Copy previous TS's sql file to get your previous Teamspeak on New Server.
