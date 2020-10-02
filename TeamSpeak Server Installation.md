# TeamSpeak Server Installation

 - First download Linux 64 bit server from [here](https://www.teamspeak.com/en/downloads/#server).
 - Copy it to Desktop. Extract it. Rename it as teamspeak. So the directory is /home/<user>/Desktop/TeamSpeakServer/
 - Open a terminal inside the **teamspeak** folder and type these commands.
   ```




Copy these lines into teamspeak.service file :

[Unit]
Description=TeamSpeak 3 Server
After=network.target
[Service]
WorkingDirectory=/home/yunus/Desktop/teamspeak/
User=yunus
Group=yunus
Type=forking
ExecStart=/home/yunus/Desktop/teamspeak/ts3server_startscript.sh start inifile=ts3server.ini
ExecStop=/home/yunus/Desktop/teamspeak/ts3server_startscript.sh stop
PIDFile=/home/yunus/Desktop/teamspeak/ts3server.pid
RestartSec=15
Restart=always
[Install]
WantedBy=multi-user.target

Press CTRL+X -> Y -> Enter

Now write these commands :

	sudo systemctl enable teamspeak.service
	sudo systemctl start teamspeak.service

Check if running :

	service teamspeak status



Copy previous TS's sql file to get your previous Teamspeak on New Server.
