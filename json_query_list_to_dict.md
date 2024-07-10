# Convert flat list to dict

## Source data
```
thevipporfiles: 
- 'http'
- 'tcp'
```

## Ansible Command

```
jquery: '[].[{name: @, context: `"client-side"`},{name: @, context: `"server-side"`} | to_nice_yaml ]'
c_profiles: "{{ thevipporfiles | json_query(jquery) | flatten }}"
```

## Output

```
- context: "client-side"
  name: "http"
- context: "server-side"
  name: "http"
- context: "client-side"
  name: "tcp"
- context: "server-side"
  name: "tcp"
```
**Note:** ***to_nice_yaml*** is only to display output nicely
