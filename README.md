# lite-zabbix-compose
## docker-compose.yml for Zabbix 6.4

### For setup:

    # docker compose [--profile <prof_type>] [--profile <prof_type>] up -d
    or
    # COMPOSE_PROFILES=<prof_type>[,<prof_type>] docker compose up

    where <prof_type>:
        all-64 -> select all for DB type mysql and version 6.4
        agent-64 -> select agent and trapper version 6.4
        mysql-64 | pgsql-64 -> select zabbix server, nginx and DB for zabbix-6.4-latest (default)

Example:

    For full setup zabbix-mysql 6.4:
        # docker compose --profile all-64 up -d
    For full setup zabbix-pgsql 6.4:
        # docker compose --profile pgsql-64 --profile agent-64 up -d
      or
        # COMPOSE_PROFILES=pgsql-64,agent-64 docker compose up
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
