# Other Jinja2 tools

## Source data
```
app_suffix: "-1"
apps:
  - app: app1
    vs: vs1
  - app: app2
    vs: vs2
```

## append suffix to list items

### Ansible code
```
{{ apps | map(attribute='app') | product([app_suffix]) | map('join') }}
```
### Output

```
['app1-1', 'app2-1']
```
