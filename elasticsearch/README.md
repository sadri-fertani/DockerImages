```
openssl rand -base64 24 | tr -dc 'A-Za-z0-9' | head -c32
```