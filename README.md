# Deploy Authentik

Part of the [*Komodo Hub* collection.](https://github.com/komodo-hub/komodo-hub)

Runs Authentik using their default setup.

https://docs.goauthentik.io/docs/install-config/install/docker-compose

## Komodo Resource TOML

```toml
[[stack]]
name = "authentik"
[stack.config]
repo = "komodo-hub/deploy-authentik"
environment = """
  ## https://github.com/goauthentik/authentik/pkgs/container/server/versions?filters%5Bversion_type%5D=tagged
  AUTHENTIK_TAG = latest
  AUTHENTIK_SECRET_KEY = [[AUTHENTIK_SECRET_KEY]]
	
  ## Configure custom ports
	COMPOSE_PORT_HTTP = 9000
	COMPOSE_PORT_HTTPS = 9443

  ## Configure directories
  MEDIA_PATH = ./media
  TEMPLATE_PATH = ./custom-templates
  CERTS_PATH = ./certs
	
  ## Configure Postgres connection
  PG_PASS = [[AUTHENTIK_PG_PASS]]
  PG_USER = authentik
  PG_DB = authentik

  ## Container options
  RESTART = unless-stopped
  LOGGING_DRIVER = local
"""

[[variable]]
name = "AUTHENTIK_SECRET_KEY"
value = "your_secret_key"

[[variable]]
name = "AUTHENTIK_PG_PASS"
value = "your_pg_pass"
```