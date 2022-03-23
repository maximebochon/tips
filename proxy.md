# Internet Proxy Configuration

In sections below, variables like `${VARIABLE}` should be replaced with something of the form described in this table:

| Variable      | Form                                                     | Example                     |
|---------------|----------------------------------------------------------|-----------------------------|
| `HTTP_PROXY`  | `http://$username:$password@$proxy-host:$proxy-port/`    | `http://10.31.255.65:8080/` |
| `HTTPS_PROXY` | `http(s)://$username:$password@$proxy-host:$proxy-port/` | `http://10.31.255.65:8080/` |
| `NO_PROXY`    | `$host-or-IPv4-or-IPv6,...,$etc`                         | `localhost,127.0.0.1,::1`   |

&nbsp;

## [APT](https://en.wikipedia.org/wiki/APT_%28software%29)

File: `/etc/apt/apt.conf.d/proxy.conf`

Syntax:

```js
Acquire {
  http::Proxy "${HTTP_PROXY}";
  https::Proxy "${HTTPS_PROXY}";
}
```

&nbsp;

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
