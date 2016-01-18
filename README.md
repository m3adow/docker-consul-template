# docker-consul-template
This is a container for docker running [consul-template](https://github.com/hashicorp/consul-template) by Hashicorp with an
additional installation of curl.

## Features
There are only two features worth mentioning:
* **Freshness:** Every time the container is built, the newest version of consul-template
is downloaded and unpacked.
* **curl:** To enable reasonable use of the `command` directive within `template` sections, curl is preinstalled. 
This way it's easy to query the Docker socket or APIs after a template change. Example:

```HCL
template {
  source = "/mnt/templates/nginx.ctmpl"
  destination = "/mnt/nginx/nginx.conf"
  command = "curl --unix-socket /tmp/docker.sock -X POST http:/containers/nginx/kill?signal=SIGHUP"
  perms = 0600
  backup = true
}
```
