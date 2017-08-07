# kubestash

Push Credstash secrets to Kubernetes.

## installing

```
pip3 install kubestash
```

## installing - known issues

There's a known issue with the `kubernetes` library: https://github.com/kubernetes-incubator/client-python#sslerror-on-macos

which causes some people with older versions of python to get an ssl error:

```
SSLError(SSLError(1, u'[SSL: TLSV1_ALERT_PROTOCOL_VERSION] tlsv1 alert protocol version (_ssl.c:590)'),)
```

I recommend updating `openssl` and reinstalling `python3` to fix this:

```
brew update
brew install openssl
brew uninstall python3
brew install python3
```

you can also subvert the issue by using a proxy:

```
kubectl proxy -p 8080
kubestash --proxy 127.0.0.1:8080 table secret
```

## usage

```
usage: kubestash [-h] [-v] [-f] table secret

pulls secrets from Credstash and stores them in Kubernetes secret

positional arguments:
  table          credstash table you want to pull credentials from
  secret         name of the kubernetes secret you want to store secrets in

optional arguments:
  -h, --help     show this help message and exit
  -v, --verbose  verbose output
  -f, --force    replace a secret if it already exists
```
