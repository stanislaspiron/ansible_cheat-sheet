# map operators

## Source data
```
expired_certificates:
- cert1
- cert2
- cert3

used_certificates:
- cert1
- cert3
```

## equalto

### Ansible code
```
{{ expired_certificates | reject('equalto', 'cert1') }}
```
### Output

```
['cert2', 'cert3']
```
## compare

### Ansible code
```
{{ expired_certificates | reject('>', 'cert2') }}
```
### Output

```
['cert1', 'cert2']
```
## In list
### Ansible code
```
{{ expired_certificates | reject('in', used_certificates) }}
```

### Output

```
['cert2']
```
