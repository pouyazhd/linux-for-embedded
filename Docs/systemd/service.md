# systemd-service

Service files are located in 3 separate localtions:

1. /etc/systemd/system/  (prime directory)
2. /lib/systemd/system/
3. /run/systemd/system/

Mostly users add their service unit files at prime directory `/etc/systed/system/<service-name>.service`. There are two more locations which you can [READ MORE](https://medium.com/@liwp.stephen/where-to-put-the-systemd-configuration-files-da499a7b286c) about them.

> The suffix `.service` is important.

## Architecture of a serivice unit file

The service files are basically text files in `.ini` structure like:

```text
[Unit]
Description=
After=
Requires=
AssertPathExists=
StartLimitIntervalSec=
StartLimitBurst=

[Service]
Type=
Restart=
RestartSec=
User=
Group=
ExecStart=
ExecStop=

[Install]
WantedBy=
```

Three main sections are `Unit`, `Service` and `Install` and each section has it's own parts.

> These sections are case sesitive, therfore it is better to copy from web :D

**Unit**:

* **Description**: A text to show the user what does this service file do.
* **Before**: This service rub before which service.
* **After**: This service run after which service.
* **Require**: Similar to `Wants=`, but declares a stronger requirement dependency.
* **AssertPathExist**: The path wich must exists to run the service.
* **StartLimitIntervalSec**: Configure unit start rate limiting.
* **StartLimitBurst**: how many starts per interval are allowed.

> Configure unit start rate limiting. Units which are started more than burst times within an interval time span are not permitted to start any more. Use StartLimitIntervalSec= to configure the checking interval and StartLimitBurst= to configure how many starts per interval are allowed.

**Service**:

* **Type**: Configures the mechanism via which the service notifies the manager that the service start-up has finished. One of `simple`, `exec`, `forking`, `oneshot`, `dbus`, `notify`, `notify-reload`, or `idle`.
* **Restart**: Restart policy if service failed. Takes one of `always`, `no`, `on-success`, `on-failure`, `on-abnormal`, `on-watchdog` or `on-abort` values.
* **RestartSec**: Sleep time before the service restarts
* **User**: The user which service belog to.
* **Group**: The group which service belong to.
* **ExecStart**: The command to execute when we want to run the application.
* **ExecStop**: The command to execute when we want to stop the application.

**Install**:

* **WantedBy**: A list of units that depend on the unit.

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
cd /home/user/
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
sudo chmod +x /home/user/print-time.sh
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
Description="A simple service to logs the time and date of system into  
After=network.target

[Service]
Type=exec
Restart=always
ExecStart=/bin/bash /home/user/print-time.sh

[Install]
WanterBy=multi-user.target
```

### `start` and `enable` the service

> Whenever a unit file `add`, `remove` or changed by the users, systemd daemon must be reload *manually* in order to systemd understand the changes. In professional applications, the developers handle it automatically; Therefore you don't need to reload systemd daemon.

```bash
systemctl daemon-reload
```

To start the service, we use `systemctl` command:

```bash
systemctl start print-time.service
```

> sometimes start and falied with `(code=exited, status=203/EXEC)`; This mean the program/script cannot be started.

By getting `systemctl status` of the service, we can see how does it work, where does it locate and the logs of service.

```bash
systemctl status pritn-time
```

If we want our service run automatically when the systemd booted( or by the conditions the user add to service file), we have to enable it.

```bash
systemctl enable print-time
```

### see the logs and outputs

The logs of this script will be written into syslog. use `journalctl` command to see the logs.

```bash
journalctl -exu print-time.service
```

## Stop and disable the service

systemd also predict the commands when you want to `stop` or `disable` it.

Stopping the service is just like starting it, except pass `stop` option to `systemctl`.

```bash
systemctl stop print-time
```

To disable it:

```bash
systemctl disable print-time
```

## Sources

* Arch linux documentry -- [systemd.unit](https://man.archlinux.org/man/systemd.unit.5.en)
* Arch linux documentry -- [systemd.service](https://man.archlinux.org/man/systemd.service.5.en)
* Redhat documentation -- [Working with systemd unit files](https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/9/html/using_systemd_unit_files_to_customize_and_optimize_your_system/assembly_working-with-systemd-unit-files_working-with-systemd#assembly_working-with-systemd-unit-files_working-with-systemd)
* Freedesktop -- [systemd syntax](https://www.freedesktop.org/software/systemd/man/latest/systemd.syntax.html#)
