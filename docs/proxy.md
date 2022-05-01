Taken from https://inside-docupedia.bosch.com/confluence/pages/viewpage.action?pageId=2055829490

Update Docker Desktop Settings
Go to ```Settings > Resources > Proxies``` and add the following proxy information.

Web Server (HTTP)|	```http://host.docker.internal:3128```	

Secure Web Server (HTTPS)|	```http://host.docker.internal:3128```    Or check "Use same for both."

Bypass for these hosts|	```host.docker.internal,localhost,127.0.0.1,.bosch.com```	No wildcards * allowed.


Update Docker ```config.json```

Open your `````~/.docker/config.json````` and change the proxy settings here as well. For reference, mine looks like this:
```
{
  "auths": {},
  "credsStore": "desktop",
  "currentContext": "default",
  "proxies": {
    "default": {
      "httpProxy": "http://host.docker.internal:3128",
      "httpsProxy": "http://host.docker.internal:3128"
    }
  },
  "stackOrchestrator": "swarm"
}
```