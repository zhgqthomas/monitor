# APItools Traffic Monitor [![Build Status](https://travis-ci.org/APItools/monitor.svg?branch=master)](https://travis-ci.org/APItools/monitor)

APITools is a hosted proxy mainly for API calls, but can be used as a general programmable proxy.
It has analytics, lua middleware, storing passed calls and many other features.

# Building and Developing
This branch can only built by docker. Other ways please check out [branch onpremise](https://github.com/zhgqthomas/monitor/tree/onpremise).

## Docker

```bash
docker-compose up -d
```

# iptables firewall port 7021
One of the most annoying things with Docker has been how it interacts with iptables. Thanks to [this article](https://unrouted.io/2017/08/15/docker-firewall/) to solve this problem.


