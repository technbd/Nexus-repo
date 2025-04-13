## Nexus Repository Manager:

Nexus Repository Manager is a repository management tool developed by Sonatype. It is used to store, manage, and distribute software artifacts, dependencies, and containers in a secure and efficient manner.

New Nexus Repository version 3.71.0 installations and above default to using an **embedded H2 database**. For production deployments larger than the minimum usage, we highly recommend using PostgreSQL databases.

There are two editions:
- Nexus Repository OSS (Open Source) – Free and community-supported.
- Nexus Repository Pro – Paid version with advanced features like high availability, role-based access control, and support.



#### Prerequisites:

- Java
- CPU: 2+ Cores, RAM: 4 GB
- Port 8081 open


```
java -version
```


### Download Nexus Repository Manager:

```
cd /opt

wget https://download.sonatype.com/nexus/3/nexus-3.79.1-04-linux-x86_64.tar.gz
```


```
tar -xvf nexus-3.79.1-04-linux-x86_64.tar.gz
```


```
mv nexus-3.79.1-04 nexus
```


#### Configure Nexus Repository Manager: 


_For security, create a dedicated `nexus` user:_

```
useradd nexus
```


_Give permission to nexus files and nexus directory to `nexus` user:_

```
chown -R nexus:nexus /opt/nexus
chown -R nexus:nexus /opt/sonatype-work
```



```
vim /opt/nexus/bin/nexus


run_as_user='nexus'
```


```
vim /opt/nexus/bin/nexus.vmoptions

-Xms2048m
-Xmx2048m
-XX:MaxDirectMemorySize=2048m
```



```
vim /opt/sonatype-work/nexus3/etc/nexus.properties


application-port=8081
application-host=0.0.0.0
```




#### Start the Nexus:

```
./bin/nexus start

./bin/nexus stop
```




### Run Nexus as a service using Systemd:

To run nexus as service using Systemd:

```
vim /etc/systemd/system/nexus.service


[Unit]
Description=nexus service
After=network.target

[Service]
Type=forking
LimitNOFILE=65536

ExecStart=/opt/nexus/bin/nexus start
ExecStop=/opt/nexus/bin/nexus stop

User=nexus
Restart=on-abort

[Install]
WantedBy=multi-user.target
```


```
systemctl daemon-reload

systemctl start nexus
systemctl restart nexus
systemctl status nexus
```


### Access Nexus Web UI:

Once Nexus is running, open a web browser and go to: `http://<server-ip>:8081`

- Username: admin
- Password: (from the file above)


```
cat /opt/sonatype-work/nexus3/admin.password
```




### Links:
- [Nexus Repository System Requirements](https://help.sonatype.com/en/sonatype-nexus-repository-system-requirements.html)
- [Nexus Repo Download](https://help.sonatype.com/en/download.html)
- [Install Nexus Repository Manager](https://www.atlantic.net/dedicated-server-hosting/how-to-install-sonatype-nexus-repository-manager-on-oracle-linux-8/)
- [Install Nexus Repository Manager on Ubuntu](https://www.howtoforge.com/how-to-install-nexus-repository-manager-on-ubuntu-22-04/)









