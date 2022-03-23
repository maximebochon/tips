# Internet Proxy Configuration

## [APT](https://en.wikipedia.org/wiki/APT_%28software%29)

File: `/etc/apt/apt.conf.d/proxy.conf`

Syntax:

```sh
Acquire {
  http::Proxy "${HTTP_PROXY}";
  https::Proxy "${HTTPS_PROXY}";
}
```

# [Docker](https://en.wikipedia.org/wiki/Docker_(software))

File: `/etc/systemd/system/docker.service.d/proxy.conf`

Syntax:

```ini
[Service]
Environment="HTTP_PROXY=${HTTP_PROXY}"
Environment="HTTPS_PROXY=${HTTPS_PROXY}"
Environment="NO_PROXY=${NO_PROXY}"
```

Reload procedure:

```sh
sudo systemctl daemon-reload
sudo systemctl restart docker.service
```
