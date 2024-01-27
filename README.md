# lite-zabbix-compose
## docker-compose.yml for Zabbix 6.4

### For setup:

    # docker compose [--profile <prof_type>] [--profile <prof_type>] up -d
    Or
    # COMPOSE_PROFILES=<prof_type>[,<prof_type>] docker compose up

    where <prof_type>:
        all-64 -> select all for DB type mysql and version 6.4
        agent-64 -> select agent and trapper version 6.4
        mysql-64 | pgsql-64 -> only zabbix server, nginx and DB for zabbix-6.4-latest (default)

Example:

    For full setup zabbix-mysql 6.4:
        # docker compose --profile all-64 up -d
    For setup zabbix-6.4 (only servers)
        # docker compose up -d

### For update image to latest version:

    # docker compose [--profile <prof_type>] [--profile <prof_type>] pull
    # docker compose [--profile <prof_type>] [--profile <prof_type>] up -d
    Or
    # COMPOSE_PROFILES=<prof_type>[,<prof_type>] docker compose pull
    # COMPOSE_PROFILES=<prof_type>[,<prof_type>] docker compose up -d

Example:
    # docker compose --profile agent-64 pull -d
    # docker compose --profile agent-64 up -d
