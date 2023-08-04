# Add default value in list of dicts

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

## Ansible Command

```
{{ clientssl | json_query('[*].[cert,chain,caFile,clientCertCa]') | flatten | unique | to_nice_json}}
```

## Output

```
[
    "default.crt",
    "ca_bundle.crt",
    "ca_clients_bundle.crt",
    "app1.crt"
]
```
**Note:** ***to_nice_json*** is only to display output nicely
