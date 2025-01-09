# lite-zabbix-compose
## docker-compose.yml for Zabbix 7.0 6.4

### For setup:

    # docker compose [--profile <prof_type>] [--profile <prof_type>] up -d
    or
    # COMPOSE_PROFILES=<prof_type>[,<prof_type>] docker compose up

    where <prof_type>:
        all-64 -> Select zabbix-server DB type mysql. zabbix-proxy DB mysql3. All version 6.4
        agent-64 -> Select agent and trapper version 6.4
        agent-7  -> Select agent and trapper version 7.0
        mysql-64 | pgsql-64 -> zabbix server, nginx DB for zabbix-6.4
        proxy-sqlite-64 | proxy-mysql-64 -> Select zabbix proxy server DB for zabbix-6.4

    If you do not specify a profile, they will be installed:
        mysql-server, zabbix-server-mysql, zabbix-web-nginx-mysql for zabbix-6.4

Example:

    For full setup zabbix-mysql 6.4:
        # docker compose --profile all-64 up -d

    For full setup zabbix-pgsql 6.4:
        # docker compose --profile pgsql-64 --profile agent-64 --profile proxy-sqlite-64 up -d
      or
        # COMPOSE_PROFILES=pgsql-64,agent-64,proxy-sqlite-64 docker compose up

    For setup zabbix-6.4 (only servers)
        # docker compose up -d

### For update image to latest version:

    # docker compose [--profile <prof_type>] [--profile <prof_type>] pull
    # docker compose [--profile <prof_type>] [--profile <prof_type>] up -d
    or
    # COMPOSE_PROFILES=<prof_type>[,<prof_type>] docker compose pull
    # COMPOSE_PROFILES=<prof_type>[,<prof_type>] docker compose up -d

Example:

    # docker compose --profile agent-64 pull -d
    # docker compose --profile agent-64 up -d

After starting the zabbix-server, for the zabbix-agent to work correctly, set the following interface values in the Host 'Zabbix server' settings:

    DNS name: zabbix-agent
    Connect to: DNS
