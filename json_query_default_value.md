# Add default value in list of dicts

## Source data
```
{
  "members": [
    {
        "ip": "1.1.1.1",
        "priority": 10
    },
    {
        "ip": "1.1.1.2",
        "port": 80
    },
    {
        "ip": "1.1.1.3",
        "port": 8080
    }
  ]
}
```

## Ansible Command

```
{{ members | json_query('[].merge(`{"port": 443, "priority": 20}`, @)') | to_nice_json }}
```

## Output

```
[
    {
        "ip": "1.1.1.1",
        "port": 443,
        "priority": 10
    },
    {
        "ip": "1.1.1.2",
        "port": 80,
        "priority": 20
    },
    {
        "ip": "1.1.1.3",
        "port": 8080,
        "priority": 20
    }
]
```
