# lite-zabbix-compose
## docker-compose.yml for Zabbix 6.4 / 7.0 / MySQL/PostgreSQL, Nginx, Agent, Trapper, Proxy


## Notes
1. If you plan to install proxy server together with zabbix-server in one docker configuration, you need to comment out port parameter **"- 10051:10051"** for service **"zabbix-server-..."** in docker-compose.yaml file before running docker-compose.



2. Also in this case, after installing the configuration, you need to add **Proxy Server** with the following parameters:

> Create proxy<br>
> Set "Proxy name": zabbix-proxy


## For setup:

    # docker compose [--profile <prof_type>] [--profile <prof_type>] up -d
    or
    # COMPOSE_PROFILES=<prof_type>[,<prof_type>] docker compose up


Where <prof_type>

| <prof_type>* | Version |Zabbix Server|DB Server|Zabbix NGINX|Zabbix proxy**|Zabbix agent|Zabbix trapper|
|:-------------|:-------:|:-----------:|:-------:|:----------:|:------------:|:----------:|:------------:|
| `Complect`   |         |             |         |            |              |            |              |
| * If no set  |7.0 MySQL| +           | +       | +          |              |            |              |
| all-7        |7.0 MySQL| +           | +       | +          | + `**SQLite` | +          | +            | 
| all-64       |6.4 MySQL| +           | +       | +          | + `**SQLite` | +          | +            |
| `By DB type` |         |             |         |            |              |            |              |
| mysql-7      |7.0 MySQL| +           | +       | +          |              |            |              |
| pgsql-7      |7.0 PgSQL| +           | +       | +          |              |            |              |
| mysql-64     |6.4 MySQL| +           | +       | +          |              |            |              |
| pgsql-64     |6.4 PgSQL| +           | +       | +          |              |            |              |
| `Agent`      |         |             |         |            |              |            |              |
| agent-7      |7.0      |             |         |            |              | +          | +            |
| agent-64     |6.4      |             |         |            |              | +          | +            |
| `Proxy`        |          |          |         |            |              |            |              |
| proxy-sqlite-7 |7.0 SQLite|          |         |            | +            |            |              |
| proxy-mysql-7  |7.0 MySQL |          |         |            | +            |            |              |
| proxy-sqlite-64|6.4 SQLite|          |         |            | +            |            |              |
| proxy-mysql-64 |6.4 MySQL |          |         |            | +            |            |              |


	If you do not specify a profile, they will be installed:
       # mysql-server, zabbix-server-mysql, zabbix-web-nginx-mysql for zabbix-7.0



#### Example:

    For full setup zabbix-mysql 6.4:
        # docker compose --profile all-64 up -d

    For full setup zabbix-pgsql 7.0:
        # docker compose --profile pgsql-7 --profile agent-7 --profile proxy-sqlite-7 up -d
      or
        # COMPOSE_PROFILES=pgsql-7,agent-7,proxy-sqlite-7 docker compose up

    For setup zabbix-7.0 (only servers)
        # docker compose up -d

### For update image to latest version:

    # docker compose [--profile <prof_type>] [--profile <prof_type>] pull
    # docker compose [--profile <prof_type>] [--profile <prof_type>] up -d
    or
    # COMPOSE_PROFILES=<prof_type>[,<prof_type>] docker compose pull
    # COMPOSE_PROFILES=<prof_type>[,<prof_type>] docker compose up -d

#### Example:

    # docker compose --profile agent-7 pull -d
    # docker compose --profile agent-7 up -d





## Fixing errors:

`Host Zabbix server: Agent not Availability`

For Host 'Zabbix server' settings:
> "DNS name": zabbix-agent<br>
> "Connect to": DNS


`In the docker log zabbix-agent there is an error:`
and
`In the docker log zabbix-server there is an error:` 

	... no active checks on server [zabbix-server:10051]: host [zabbix-server] not found
	... cannot send list of active checks to ...

> Rename Host 'Zabbix server' to 'zabbix-server'


`In the docker log zabbix-server is an error:`
and
`In the docker log zabbix-proxy is an error:`

	... cannot send proxy data to server at "zabbix-server"
	... cannot parse proxy data from active proxy at ...

> Create proxy<br>
> Set "Proxy name": zabbix-proxy

