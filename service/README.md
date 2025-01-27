# thold daemon installation

## Introduction

The thold daemon was designed to improve Cacti's scalability by allowing the
thold check process to take place out of band.  By doing so, the time Cacti
spends checking thresholds can be reduced significantly.  This service folder
includes initialization scripts for both systemd and initd based systems.  To
install the thold daemon as a service, follow the instructions below.

## SystemD Based Systems

Follow the steps below to install the thold daemon on a SystemD system.

* Verify the location of the thold_daemon.php in the systemd subfolder of the
  location of this README.md file.

* You may have to change mariadb.service to mysql.service depending on your
  installed version of MariaDB or MySQL.

* Update the <CACTIPATH> to point to you Cacti base path.

* Copy the `thold_daemon.service` file to systemd directory and then reload the
  systemd daemon so that it knows the new service is available.

  ```shell
  cp thold_daemon.service /etc/systemd/system
  systemctl daemon-reload
  ```

* Edit the `thold_daemon.service` file and update the ExecStart/ExecStop paths
  with the location of the `thold_daemon` shell script.  By default, this script
  is found in the [cacti]/plugin/thold/service/systemd folder, but the service
  file is currently hardcoded to expect [cacti] is located at:

  /var/www/html/cacti

* Ensure that the `thold_daemon` script is marked executable

  ```shell
  chmod +x thold_daemon.php
  ```

* Enable and start the service using either the -now parameter:

  ```shell
  systemctl enable --now thold_daemon
  ```

  or issuing two separate commands if you want to start at a later date:

  ```shell
  systemctl enable thold_daemon
  systemctl start thold_daemon
  ```

* Running on Windows?  Switch to Linux!

* System V init?  Upgrade your Linux!

-----------------------------------------------
Copyright (c) 2004-2023 - The Cacti Group, Inc.
