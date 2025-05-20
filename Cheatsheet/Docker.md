# Command
| Command                    | Description                |
| -------------------------- | -------------------------- |
| docker ps -a               | List all containers        |
| docker image prune -a      | Remove all unused images   |
| docker logs -f [container] | Show real-time update logs |
# HealthCheck
```yml
services:
	app:
		build: .
		healthcheck:
			test:["CMD", "curl", "-f", "http://localhost:3000"]
			interval: 30s
			timeout: 5s
			retries: 3
```
> [!info]
> Add [Auto Heal](https://github.com/willfarrell/docker-autoheal) to monitor and restart unhealthy containers