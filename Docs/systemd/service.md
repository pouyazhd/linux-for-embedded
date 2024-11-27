# systemd-service

Service files are located in 3 separate localtions:

1. /etc/systemd/system/  (prime directory)
2. /lib/systemd/system/
3. /run/systemd/system/

Mostly users add their service unit files at prime directory `/etc/systed/system/<service-name>.service`. There are two more locations which you can [READ MORE](https://medium.com/@liwp.stephen/where-to-put-the-systemd-configuration-files-da499a7b286c) about them.

> The suffix `.service` is important.

## Architecture of a serivice unit file

The service files are basically text files.

```text
[Unit]
Description=
After=
Requires=
AssertPathExists=
StartLimitIntervalSec=0

[Service]
Type=
Restart=
RestartSec=
User=
Group
ExecStart=
ExecStop=
PrivateTmp=

[Install]
WantedBy=
```

Three main sections are `Unit`, `Service` and `Install` and each section has it's own parts.

> These sections are case sesitive, therfore it is better to copy from web :D

**Unit**:

* **Description**: A text to show the user what does this service file do.
* **Before**: This service rub before which service.
* **After**: This service run after which service.

**Service**:

* **Type**:
* **Restart**: Restart policy if service failed. Takes one of `always`, `no`, `on-success`, `on-failure`, `on-abnormal`, `on-watchdog` or `on-abort` values.

## Example

Steps:

1. create a simple bash script (or any thing else)
2. create a service file at `/etc/systemd/system/`
3. `star` and `enable` it.
4. see the logs and outputs

### create a simple bash script

At home directory we create a bash script to output the system time.

```bash
# create a print-time.sh file at home directory
cd ~/
vim print-time.sh
```

Write the script we want to run:

```bash
#! /bin/bash
while true;
  do
    date;
    sleep 1;
  done
```

Make it executable:

```bash
sudo chmod +x ~/print-time.sh
```

### create a service file to print-time

At `/etc/systemd/system/`, create a service file named `print-time.service`.

```bash
cd /etc/systemd/system/
sudo vim print-time.service
```

> name of the service can be anything but it is better to be similar to the name of the application we want to run.

Now create a service file:

```text
[Unit]

[Service]

[Install]
WanterBy=multi-user.target
After=

```
