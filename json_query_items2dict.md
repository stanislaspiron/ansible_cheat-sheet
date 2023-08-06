# Add default value in list of dicts

## Source data
```
services: |
  service1 1h up some useless values
  service2 1h down some other useless values
  service3 1h up
```

## Ansible Command

```
{{ services
      | split('\n')
      | map('split')
      | json_query('[*].{name: [0], status: [2]}')
      | to_nice_yaml
    }}
```
## Output

```
-   name: service1
    status: up
-   name: service2
    status: down
-   name: service3
    status: up
```
**Note:** ***to_nice_yaml*** is only to display output nicely
