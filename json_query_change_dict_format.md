# Change dict format and key names

## Source data
```
clientssl:
-   caFile: ca_clients_bundle.crt
    keyCertChain:
      cert: default.crt
      chain: ca_bundle.crt
      key: default.key
    clientCertCa: ca_clients_bundle.crt
    name: clientssl1
-   caFile: ca_clients_bundle.crt
    keyCertChain:
      cert: default.crt
      chain: ca_bundle.crt
      key: default.key
    clientCertCa: ca_clients_bundle.crt
    name: clientssl2
```

## Ansible Command

```
{{ clientssl  | json_query('[].{name: name, cert: keyCertChain[0].cert,chain: keyCertChain[0].chain  }') | to_nice_yaml }}
```

## Output

```
-   cert: default.crt
    chain: ca_bundle.crt
    name: clientssl1
-   cert: default.crt
    chain: ca_bundle.crt
    name: clientssl2
```
**Note:** ***to_nice_yaml*** is only to display output nicely
