# Group list items by key

## Source data
```
mylist:
- uuid: "001"
  myValue: value1
- uuid: "002"
  myValue: value1
- uuid: "003"
  myValue: value2

```

## Ansible Command

```
{{ [mylist | json_query('[].{uuids: [uuid], myValue: myValue }'), []] 
  | community.general.lists_mergeby('myValue', list_merge='append') 
  | to_nice_yaml 
}}

```

## Output

```
-   myValue: value1
    uuids:
    - '001'
    - '002'
-   myValue: value2
    uuids:
    - '003'
```
**Note:** ***to_nice_yaml*** is only to display output nicely
