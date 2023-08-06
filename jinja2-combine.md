# Combine

## Source data
```
clientssl:
  profile1:
    caFile: ca_clients_bundle.crt
    keyCertChain:
      cert: default.crt
      chain: ca_bundle.crt
      key: default.key
    clientCertCa: ca_clients_bundle.crt
    name: clientssl1
  profile2:
    caFile: ca_clients_bundle.crt
    keyCertChain:
      cert: default.crt
      chain: ca_bundle.crt
      key: default.key
    clientCertCa: ca_clients_bundle.crt
    name: clientssl2

new_profile:
    caFile: ca_clients_bundle.crt
    keyCertChain:
      cert: default.crt
      chain: ca_bundle.crt
      key: default.key
    clientCertCa: ca_clients_bundle.crt
    name: clientssl3

update_profile:
    keyCertChain:
      chain: default.crt
```

## New object or replace object with same key

### Ansible code
```
{{ clientssl  | combine({"profile3": new_profile }) | to_nice_yaml}}
```
### Output

```
profile1:
    caFile: ca_clients_bundle.crt
    clientCertCa: ca_clients_bundle.crt
    keyCertChain:
        cert: default.crt
        chain: ca_bundle.crt
        key: default.key
    name: clientssl1
profile2:
    caFile: ca_clients_bundle.crt
    clientCertCa: ca_clients_bundle.crt
    keyCertChain:
        cert: default.crt
        chain: ca_bundle.crt
        key: default.key
    name: clientssl2
profile3:
    caFile: ca_clients_bundle.crt
    clientCertCa: ca_clients_bundle.crt
    keyCertChain:
        cert: default.crt
        chain: ca_bundle.crt
        key: default.key
    name: clientssl3
```
## Update a single value in nested dict

### Ansible code
```
{{ clientssl  | combine({"profile2": update_profile }, recursive=true) | to_nice_yaml}}
```
### Output

```
profile1:
    caFile: ca_clients_bundle.crt
    clientCertCa: ca_clients_bundle.crt
    keyCertChain:
        cert: default.crt
        chain: ca_bundle.crt
        key: default.key
    name: clientssl1
profile2:
    caFile: ca_clients_bundle.crt
    clientCertCa: ca_clients_bundle.crt
    keyCertChain:
        cert: default.crt
        chain: default.crt
        key: default.key
    name: clientssl2
```
