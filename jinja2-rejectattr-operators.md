# reject / select operators

## Source data
```
apps:
  - app: app1
    vs: vs1
    pool:
     port: 443
     members: 
     - 1.1.1.1
     - 1.1.1.2
  - app: app2
    vs: vs2
    pool:
     port: 80
     members: 
     - 1.1.2.1
     - 1.1.2.2
```

## equalto

### Ansible code
```
{{ apps | selectattr('pool', 'defined') | selectattr('pool.port', 'defined') | selectattr('pool.port', 'equalto', 80) | to_nice_json }}
```
### Output

```
[
    {
        "app": "app2",
        "pool": {
            "members": [
                "1.1.2.1",
                "1.1.2.2"
            ],
            "port": 80
        },
        "vs": "vs2"
    }
]
```
## compare

### Ansible code
```
{{ apps | selectattr('pool', 'defined') | selectattr('pool.port', 'defined') | selectattr('pool.port', '>', 100) | to_nice_json }}
```
### Output

```
[
    {
        "app": "app1",
        "pool": {
            "members": [
                "1.1.1.1",
                "1.1.1.2"
            ],
            "port": 443
        },
        "vs": "vs1"
    }
]
```
## In list
### Ansible code
```
{{ apps | selectattr('pool', 'defined') | selectattr('pool.port', 'defined') | selectattr('pool.port', 'in', [22,80]) | to_nice_json }}
```

### Output

```
[
    {
        "app": "app2",
        "pool": {
            "members": [
                "1.1.2.1",
                "1.1.2.2"
            ],
            "port": 80
        },
        "vs": "vs2"
    }
]
```
