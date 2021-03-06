# OpCon on Docker
This repository provides a [docker compose](https://docs.docker.com/compose/) file to bootstrap the process of spinning up working OpCon environments.

To access the full OpCon docker image documentation (Arguments, Environment Variables...):
- [OpCon Image Documentation](https://hub.docker.com/r/smatechnologies/opcon-server)

# Disclaimer
No Support and No Warranty are provided by SMA Technologies for this project and related material. The use of this project's files is on your own risk.

SMA Technologies assumes no liability for damage caused by the usage of any of the files offered here via this Github repository.

# Prerequisites
- Docker Engine 18.06.0+
- Docker Compose 1.22+ (Compose File Format 3.7)

# Compatibility

| Docker-Compose Version  | OpCon Version  |
|-------------------------|----------------|
| 1.0.0                   | 19.1.1+        |
| 1.0.1                   | 19.1.1+        |

# Docker-Compose Instructions
Grab the **[docker-compose.yml](docker-compose.yml)** file, define your environment variables via the **.env** file and then run the following command to start MS SQL and OpCon Server containers.
```
docker-compose up
```
Note: *You must be on the same directory as your docker-compose.yml file*

**Single Line Command Execution**

Linux / macOS:
```
curl -L https://raw.githubusercontent.com/SMATechnologies/opcon-docker/1.0.2/docker-compose.yml --output docker-compose.yml && SQL_ADMIN_PASSWORD=MssqlP@ssWord42 DB_PASSWORD=OpconP@ssWord42 VOLUME_PATH=/tmp/opcon docker-compose up
```

Windows:
```
curl -L https://raw.githubusercontent.com/SMATechnologies/opcon-docker/1.0.2/docker-compose.yml --output docker-compose.yml; $env:SQL_ADMIN_PASSWORD="MssqlP@ssWord42"; $env:DB_PASSWORD="OpconP@ssWord42"; $env:VOLUME_PATH="C:\OpCon\"; docker-compose up
```

## Environment Variables

### Mandatory

```
VOLUME_PATH=c:/opcon-docker //Location of all the container data
SQL_ADMIN_PASSWORD= //MSSQL SA Password
DB_PASSWORD= //Opcon DataBase Password
```

### Recommended

```
LICENSE= //The Opcon Key License. Necessary to apply the license (See instructions below - Conversions/OpCon License Key String)
TZ=UTC //The Timezone
```

### Optional (with default Values)

```
CONTAINER_PREFIX=opcon
OPCON_REPOSITORY=smatechnologies/opcon-server (smaengineering.azurecr.io/opcon for Development)
OPCON_VERSION=19.1.1-prerelease
MSSQL_VERSION=2017-latest
MSSQL_HOSTNAME=opcon-mssql
OPCON_HOSTNAME=opcon-core
API_PORT=9010
```

Please see the full Docker Image Documentation about environment variables of Opcon Image:
- [OpCon Image Documentation](https://hub.docker.com/r/smatechnologies/opcon-server)

# Alternative Deployments

## Docker Run (Without Docker Compose)

- [OpCon Image Documentation](https://hub.docker.com/r/smatechnologies/opcon-server)

# Miscellaneous

## OpCon License Key String

How to generate key from file:
- Linux: `cat <LIC_FILE> | hexdump -ve '16/1 "%02x"' | sed 's/.*/<LIC_FILE_WITHOUT_LIC_EXT>:\0/'`
- Windows `certutil -encodehex <LIC_FILE> key.tmp 12 >NUL && echo|set /p="<LIC_FILE_WITHOUT_LIC_EXT>:" || type key.tmp && del key.tmp`

# License
Copyright 2019 SMA Technologies

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at [apache.org/licenses/LICENSE-2.0](http://www.apache.org/licenses/LICENSE-2.0)

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

# Contributing
We love contributions, please read our [Contribution Guide](CONTRIBUTING.md) to get started!

# Code of Conduct
[![Contributor Covenant](https://img.shields.io/badge/Contributor%20Covenant-v2.0%20adopted-ff69b4.svg)](code-of-conduct.md)
SMA Technologies has adopted the [Contributor Covenant](CODE_OF_CONDUCT.md) as its Code of Conduct, and we expect project participants to adhere to it. Please read the [full text](CODE_OF_CONDUCT.md) so that you can understand what actions will and will not be tolerated.
