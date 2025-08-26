# confluence


New Confluence/Jira releases support only Data Center licenses. To generate a Data Center licenses, add the `-d` parameter.

---
Please be sure to upgrade to the latest version(9.5.3 or 9.2.7), as this [bug](https://confluence.atlassian.com/security/cve-2023-22518-improper-authorization-vulnerability-in-confluence-data-center-and-server-1311473907.html).



---
[README](README.md) 

default port: 8090

+ Latest Version(arm64&amd64): v9(9.5.3)
+ LTS Version:(arm64&amd64) v8(9.2.7)

## Requirement
- docker-compose: 17.09.0+

## How to run with docker-compose

- start confluence & mysql

```
git clone https://github.com/spektrium/confluence.git \
    && cd confluence \
    && docker-compose up
```

- start confluence & mysql daemon

```
docker-compose up -d
```

- default db(mysql8.0) configure:

```bash
driver=mysql
host=mysql-confluence
port=3306
db=confluence
user=root
passwd=123456
```

## How to run with docker

- start confluence

```
docker volume create confluence_home_data && docker network create confluence-network && docker run -p 8090:8090 -v confluence_home_data:/var/confluence --network confluence-network --name confluence-srv -e TZ='Asia/Shanghai' spektrium/confluence:9.5.3
```

- config your own db:


## How to hack confluence

```
docker exec confluence-srv java -jar /var/agent/atlassian-agent.jar \
    -d \
    -p conf \
    -m Hello@world.com \
    -n Hello@world.com \
    -o your-org \
    -s you-server-id-xxxx
```

## How to hack confluence plugin

- .eg I want to use BigGantt plugin
1. Install BigGantt from confluence marketplace.
2. Find `App Key` of BigGantt is : `eu.softwareplant.biggantt`
3. Execute :

```
docker exec confluence-srv java -jar /var/agent/atlassian-agent.jar \
    -d \
    -p eu.softwareplant.biggantt \
    -m Hello@world.com \
    -n Hello@world.com \
    -o your-org \
    -s you-server-id-xxxx
```

4. Paste your license


## How to upgrade

```shell
cd confluence && git pull
docker pull spektrium/confluence:latest && docker-compose stop
docker-compose rm
```

enter `y`, then start server

```shell
docker-compose up -d
```

