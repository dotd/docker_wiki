# Windows Docker Configuration Behind Bosch Firewall

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

# Ubuntu Docker Configuration Behind Bosch Firewall 

Complied from https://inside-docupedia.bosch.com/confluence/pages/viewpage.action?pageId=2055829490 and https://connect.bosch.com/wikis/home?lang=en-us#!/wiki/Wfcca43188475_41ba_824b_b27adcc3b184/page/Docker%20in%20the%20Bosch%20Corporate%20Network.

1. If you use OSD (Ubuntu) you can just install Docker using apt. 
2. Install Kerberos using the following steps:
```
sudo apt install osd-proxy-package-experimental
cd
mkdir -p .px/
cp /opt/osd/proxy/config.de.ini .px/config.ini
```
3. Since docker is on the interface 172.17.0.1, add it to the 'binds' line of .px/config.ini, such that the file looks like this:
```
[proxy]
endpoints = rb-proxy-de.bosch.com:8080
optimize = False
renewtoken = True

[server]
binds = 172.17.0.1:3128

[logger]
level = 40
logtofile = False
```
4. You need to set the proxy for Docker daemon also using environment variable. Docker run is also doing docker pull since the image doesn't exist. In your case, the proxy is only applied to the docker run command, which delegates to the docker daemon which is running without proxy. Create a file named `/etc/systemd/system/docker.service.d/10_docker_proxy.conf` with below content:
```
[Service]
Environment="HTTP_PROXY=http://localhost:3128"
Environment="HTTPS_PROXY=http://localhost:3128"
Environment="NO_PROXY=host.docker.internal,localhost,127.0.0.1,.bosch.com"
```
5. Create a file `~/.docker/config.json` with the following content:
```
{
 "proxies":
 {
   "default":
   {
     "httpProxy": "http://localhost:3128",
     "httpsProxy": "http://localhost:3128",
     "noProxy": "host.docker.internal,localhost,127.0.0.1,.bosch.com"
   }
 }
}
```
6. When building an image, add the flag `--network=host`. For example: `docker build -t new-image --network=host .`.
