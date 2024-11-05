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
file_paths = [
  "compose.yaml",
  # "caddy.compose.yaml" # Deploy https proxy
]
environment = """
  AUTHENTIK_IMAGE = ghcr.io/goauthentik/server
  AUTHENTIK_TAG = latest
  AUTHENTIK_SECRET_KEY = [[AUTHENTIK_SECRET_KEY]]
	
  ## Configure custom ports
	COMPOSE_PORT_HTTP = 9000
	COMPOSE_PORT_HTTPS = 9443
	
  ## Configure Postgres connection
  PG_PASS = [[AUTHENTIK_PG_PASS]]
  PG_USER = authentik
  PG_DB = authentik

  ## Optional. Deploy caddy proxying to AUTHENTIK_DOMAIN
  CADDY_TAG = latest
  # Required for Caddy deploy
  AUTHENTIK_DOMAIN = authentik.example.com
"""

[[variable]]
name = "AUTHENTIK_SECRET_KEY"
value = "your_secret_key"
is_secret = true

[[variable]]
name = "AUTHENTIK_PG_PASS"
value = "your_pg_pass"
is_secret = true
```