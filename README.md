# syncer

## Generate key pair

```bash
ssh-keygen -t rsa -b 4096 syncer.id_rsa
```

## Create `authorized_keys` entry on server

```
command="cat hosts.yaml",no-port-forwarding,no-x11-forwarding,no-agent-forwarding ssh-rsa KEY-DATA HOST-INFO
```

## Licence

[MIT License][licence]

[licence]: LICENSE
