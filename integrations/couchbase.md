---
title: Couchbase Integration
tags: [integrations list]
permalink: couchbase.html
summary: Learn about the Wavefront Couchbase Integration.
---
## Couchbase Integration

Couchbase Server is an open-source, distributed  multi-model NoSQL database. This integration installs and configures Telegraf to send Couchbase metrics into Wavefront. Telegraf is a light-weight server process capable of collecting, processing, aggregating, and sending metrics to a [Wavefront proxy](https://docs.wavefront.com/proxies.html).

In addition to setting up the metrics flow, this integration also installs a dashboard. 


To see a list of the metrics for this integration, select the integration from <https://github.com/influxdata/telegraf/tree/master/plugins/inputs>.
## Couchbase Setup

This integration uses the Couchbase input plugin for Telegraf.



### Step 1. Install the Telegraf Agent

This integration uses the Couchbase input plugin for Telegraf. If you've already installed Telegraf on your server(s), you can skip to Step 2.

Log in to your Wavefront instance and follow the instructions in the **Setup** tab to install Telegraf and a Wavefront proxy in your environment. If a proxy is already running in your environment, you can select that proxy and the Telegraf install command connects with that proxy. Sign up for a [free trial](http://wavefront.com/sign-up/?utm_source=docs.vmware.com&utm_medium=referral&utm_campaign=docs-front-page){:target="_blank" rel="noopenner noreferrer"} to check it out!


### Step 2. Configure Couchbase Input Plugin


Create a file called `couchbase.conf` in `/etc/telegraf/telegraf.d` and enter the following snippet:
{% raw %}
```
# Read per-node and per-bucket metrics from Couchbase
[[inputs.couchbase]]
## specify servers via a url matching:
##  [protocol://][:password]@address[:port]
##  e.g.
##    http://couchbase-0.example.com/
##    http://admin:secret@couchbase-0.example.com:8091/
##
## If no servers are specified, then localhost is used as the host.
## If no protocol is specifed, HTTP is used.
## If no port is specified, 8091 is used.
servers = ["http://<username>:<password>@<your.couchbase.server>:8091"]
```
Replace `your.couchbase.server` with the IP of your Couchbase instance. Replace `username` and `password` with your instance's username and password.

To monitor multiple Couchbase server instances, configure the `servers` parameter with address of your Couchbase servers.

```
 servers = ["http://<username>:<password>@<your.couchbase.sever1>:8091", "http://<username>:<password>@<your.couchbase.sever2>:8091"]
```
{% endraw %}

### Step 3. Restart Telegraf

Run `sudo service telegraf restart` to restart your Telegraf agent.
