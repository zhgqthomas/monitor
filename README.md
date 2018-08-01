# APItools Traffic Monitor 

APITools is a hosted proxy mainly for API calls, but can be used as a general programmable proxy.
It has analytics, lua middleware, storing passed calls and many other features.

## Docker-based Installation

To install the APItools Monitor using Docker, you need first to [install it](http://docs.docker.io/installation/).

Check that docker is correctly installed by executing

``` bash
docker -v

```

Once docker is installed, you can install a Docker container of an APItools Monitor with the following command:

To run APItools monitor you need a redis server (which you  also have in Docker).

``` bash
docker run -d --name redis quay.io/3scale/redis
docker run -d -p 7071:7071 -p 10002:10002 --name apitools --link redis:db zhgqthomas/apitools
```

Once the Docker is up and running, you can move to the next step - [DNS configuration](#dns-configuration).

## Docker compose
Just download the `docker-compose.yml` file and run it.
```bash
docker-compose up -d
```

## DNS Configuration

APItools relies on the HTTP host to enroute the requests it receives to the correct [Service](/docs/using-services/). As a result,
your APItools monitor expects to be run in a domain name associated to an IP address. If private you will need to host your own DNS or at least deploy dnsmasq to provide some basic wildcard DNS.

This means that if you are testing things out in your server, just adding entries on your `/etc/hosts` file *will not work properly*.

So for quick-and-dirty tests you can use [xip.io](http://xip.io/), which provides DNS wildcards for everyone. So you can use `apitools.127.0.0.1.xip.io`
and that will resolve to `127.0.0.1`.

You can test it in the terminal using `dig`:

``` bash
dig  +short apitools.127.0.0.1.xip.io
dig  +short some-service-code-apitools.127.0.0.1.xip.io
```

Xip.io also provides shortcurts, so you can 'hide' the IP Address and get something like apitools.9zlhb.xip.io. Check the response of dig for the right shortcut for you.

## Testing & Port Configuration

APItools uses two ports: 7071 and 10002.

`7071` is where the web application lives - after the app is running, open

* [https://apitools.127.0.0.1.xip.io:7071](https://apitools.127.0.0.1.xip.io:7071)

You should see the "Congratulations!" page, asking you whether you want to send anonymous data to 3Scale. Choose your preference and click "Save", and you'll be ready to go.

If you are using xip.io to see the interface (change it to your TLD otherwise). Try adding a sample service and doing some sample requests, to make sure everything is ok.

We plan to introduce third one which will auto-detect if it is an app or a proxy and you can map it to the port 80.

`10002` is the proxy port. Your `curl` requests will look like this:

``` bash
curl http://some-service-code-apitools.127.0.0.1.xip.io:10002/something/or/other
```

Notice that the curl examples shown by APItools ommit the 10002 port, since the samples are meant for the on-line version.

## Thanks
- [Galen Zhao](https://github.com/galenzhao)
- [Michal Cichra](https://github.com/mikz)
