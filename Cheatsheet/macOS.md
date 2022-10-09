# Kill localhost process
For example, if the port is `localhost:8000`. run
```bash
sudo lsof -i :8000

```
Then run
```bash
kill -9 <PID>
```