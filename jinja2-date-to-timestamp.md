# Add default value in list of dicts

## Source data
```
certificates:
  json:
    items:
    - fullPath: cert1
      apiRawValues:
        expiration: "Jul 14 17:11:26 2021 GMT"
```

## Ansible Command

```
certificates_timestamp: |
  {% for cert in certificates.json['items'] %}
  - fullPath: {{ cert.fullPath }}
    expiration: {{ cert.apiRawValues.expiration }}
    expiration_timestamp: {{ (cert.apiRawValues.expiration | to_datetime('%b %d %H:%M:%S %Y GMT')).strftime('%s') }}
  {% endfor %}
```

## Output

```
certificates_timestamp: |
    - fullPath: cert1
    expiration: Jul 14 17:11:26 2021 GMT
    expiration_timestamp: 1626282686
```
