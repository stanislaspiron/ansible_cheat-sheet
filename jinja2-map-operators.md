# map operators

## Source data
```
{
    "clientssl": [
        {
            "caFile": "ca_clients_bundle.crt",
            "cert": "default.crt",
            "chain": "ca_bundle.crt",
            "clientCertCa": "ca_clients_bundle.crt",
            "name": "clientssl1"
        },
        {
            "caFile": "ca_clients_bundle.crt",
            "cert": "app1.crt",
            "chain": "ca_bundle.crt",
            "clientCertCa": "ca_clients_bundle.crt",
            "name": "clientssl2"
        }
    ]
}
```

## map attribute

### Ansible code
```
{{ clientssl | map(attribute='name') }}
```
### Output

```
['clientssl1', 'clientssl2']
```
## split and first

### Ansible code
```
{{ clientssl | map(attribute='cert') | map('split', '.') | map('first') }}
```
### Output

```
['default', 'app1']
```
## Update a single value in nested dict

### Ansible code
```
{{ clientssl  | map('combine', {"keyCertChain": {"chain": "default.crt"}} , recursive=true) | to_nice_yaml}}
```
### Output

```
-   caFile: ca_clients_bundle.crt
    clientCertCa: ca_clients_bundle.crt
    keyCertChain:
        cert: default.crt
        chain: default.crt
        key: default.key
    name: clientssl1
-   caFile: ca_clients_bundle.crt
    clientCertCa: ca_clients_bundle.crt
    keyCertChain:
        cert: default.crt
        chain: default.crt
        key: default.key
    name: clientssl2
```
