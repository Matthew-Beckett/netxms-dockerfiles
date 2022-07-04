# THIS IS NO LONGER MAINTAINED

<p align="center">
    <img src="https://avatars.githubusercontent.com/u/10434043?s=400&v=4" alt="drawing" width="200"/>
</p>

<h1 align="middle">NetXMS - Docker Images</h1>

## What is NetXMS?

**NetXMS**  is an  open-source network management system. It can be used for monitoring entire IT infrastructures, starting with SNMP-capable hardware such as switches and  routers and ending with applications on servers.

Victor Kirhenshtein and Alex Kirhenshtein are the original authors and current maintainers of NetXMS. NetXMS runs natively on  Windows,  Linux, and other  Unix variants. It is licensed  under the  [GNU General Public License](https://en.wikipedia.org/wiki/GNU_General_Public_License "GNU General Public License")  version 2 as published by the Free Software Foundation

[Source: Wikipedia](https://en.wikipedia.org/wiki/NetXMS)

# NetXMS Server Docker Image

Docker image of NetXMS Server ([www.netxms.org](http://www.netxms.org/)). Currently limited to SQLlite database. Database files and log files are located in docker volume /data.

Quickstart with

```
docker run ghcr.io/matthew-beckett/netxms_server:latest
```

# Environment variables

## NetXMS Server

-   **NETXMS_UNLOCKONSTARTUP**  - set to 1 to unlock database on each container startup (default), set to 0 to skip database unlocking
-   **NETXMS_CONFIG**  - Variable to set arbitrary config file entries to  _/etc/netxmsd.conf_. Put your configuration options here.
-   **NETXMS_STARTAGENT**  - Set to 1 to start the nxagent (default). Set to other value to disable agent startup.

## NetXMS Agent

-   **NXAGENT_CONFIG**  - Config variable to set. Put your configuration options here, for example "EnableSNMPProxy=yes\nServers=server1\nMasterServers=server1". Content of this variable will will replace the agent config file.
-   **NXAGENT_REGISTERSERVER**  - Agent registration (put your NetXMS server hostname here)
-   **NXAGENT_CONFIGSERVER**  - Config server hostname
-   **NXAGENT_LOGLEVEL**  - log level
-   **NXAGENT_PLATFORMSUFFIX**  - platform suffix
StackEdit stores your files in your browser, which means all your files are automatically saved locally and are accessible **offline!**
