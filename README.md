caddyfwd
========

Wraps `caddy` for even easier SSL forwarding.

### Usage

```
./caddyfwd [<listen_host>[:<listen_port>]] <upstream_host>[:<upstream_port>]
```

### Requirements

* [caddy](https://caddyserver.com) and `caddy trust`
* [jq](https://stedolan.github.io/jq/)

### Examples

#### Simple forward to `localhost:11111`

```
$ ./caddyfwd localhost:11111
Proxying localhost:443 -> localhost:11111
2022/03/21 14:14:50.645	INFO	admin	admin endpoint started
    {"address": "tcp/localhost:2019", "enforce_origin": false,
    "origins": ["localhost:2019", "[::1]:2019", "127.0.0.1:2019"]}
2022/03/21 14:14:50.646	INFO	serving initial configuration
```

#### Simple forward when `www.example.org` is mapped in your `/etc/hosts`

```
$ ./caddyfwd www.example.org localhost:11111
Proxying www.example.org:443 -> localhost:11111
2022/03/21 14:15:29.378	INFO	admin	admin endpoint started
    {"address": "tcp/localhost:2019", "enforce_origin": false,
    "origins": ["localhost:2019", "[::1]:2019", "127.0.0.1:2019"]}
2022/03/21 14:15:29.379	INFO	serving initial configuration
```

#### Mapping to a weird port and a nice check of your `/etc/hosts`

```
./caddyfwd www.example.net:38522 localhost:11111
warning: www.example.net missing from /etc/hosts
Proxying www.example.net:38522 -> localhost:11111
2022/03/21 14:17:23.709	INFO	admin	admin endpoint started
    {"address": "tcp/localhost:2019", "enforce_origin": false,
    "origins": ["localhost:2019", "[::1]:2019", "127.0.0.1:2019"]}
2022/03/21 14:17:23.709	INFO	serving initial configuration
```
