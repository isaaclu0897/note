#how-to, #hivemq, #linux, #centos, #matt, #installation

### Prerequisites

* yum install unzip
* yum install java-1.8.0-openjdk
* yum install java-11-openjdk

### Step by Step

1. Log in as root
```
sudo -i
```

2. Move to installtison pathcd /opt
```
cd /opt
```

3. Download package On the [HiveMQ website](https://www.hivemq.com/downloads/) OR use command as below
```
curl -O -L https://www.hivemq.com/releases/hivemq-4.5.5.zip
```

4. Extract the files
```
unzip hivemq-4.3.1.zip
```

5. remove hivemq symlink
```
rm -R hivemq
```

6. Create hivemq symlink again
```
ln -s hivemq-4.3.1 hivemq
```

7. Create a HiveMQ user
```
useradd -d /opt/hivemq hivemq

```

8. change the user of folder 
```
chown -R hivemq:hivemq hivemq*
```

9. copy license to new folder
```
cp hivemq-3.4.1/license/* hivemq-4.3.1/license
```

9. cd hivemq/bin
```
cd /opt/hivemq
```

10. give bash authority
```
chmod +x ./bin/run.sh
```

11. systemctl
```
systemctl enable hivemq

systemctl restart hivemq
```

### Remark

add system service into systemd
```
cp /opt/hivemq/bin/init-script/hivemq.service /etc/systemd/system/hivemq.service
```

Offical recommended that configure the JVM heap with 50% of the RAM that is available on the system on which you run HiveMQ.

The heap that the HiveMQ process uses can be set as a variable in the run.sh file (run.bat on Windows). Add a line with -Xmx to the variables.

Example configuration with a 4 GB heap:
```
############## VARIABLES
JAVA_OPTS="$JAVA_OPTS -Xmx4g"
```

systemctl daemon-reload

systemctl restart hivemq


* The HiveMQ Web UI has been renamed HiveMQ Control Center. <web-ui> changed to <control-center> accordingly in the configuration options. See the Control Center Guide for details about possible configuration options.

* Consequentially <mode>in-memory</mode> is no longer a configuration option. HiveMQ 4 always uses file persistence.
