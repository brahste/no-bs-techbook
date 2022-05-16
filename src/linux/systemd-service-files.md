# Service files
**Example**
```
[Unit]    
Description=IPC Daemon    
After=syslog.target network.target    

[Service]    
ExecStart=/usr/local/bin/vessel-microhard-system                                    
ExecReload=/usr/local/bin/vessel-microhard-system                                    
EnvironmentFile=/etc/vessel.env    
Restart=always    
RestartSec=5    
TimeoutSec=5    

[Install]    
WantedBy=multi-user.target
```