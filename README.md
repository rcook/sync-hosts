# syncer

## Configure

These commands should be run from a root shell using `sudo su - root`.

## Create `hosts.base`

```bash
mkdir /etc/hosts.d
cd /etc/hosts.d
cp ../hosts hosts.base
```

## Install prerequisites

```bash
apt install python-pip
pip install --user pyyaml
```

## Get script

```bash
cd /etc/hosts.d
git clone https://github.com/rcook/sync-hosts.git
```

## Create script runner

```bash
cd /etc/hosts.d
cp sync-hosts/run-sync-hosts.template ./run-sync-hosts
```

Then fix up `run-sync-hosts` for your configuration.

## Generate keys

```bash
cd /etc/hosts.d
ssh-keygen -t rsa -b 4096 -f sync-hosts.id_rsa -N ''
```

## Add keys to `authorized_keys` file on server

```bash
cd /etc/hosts.d
echo "command=\"cat hosts.yaml\",no-port-forwarding,no-x11-forwarding,no-agent-forwarding $(cat sync-hosts.id_rsa.pub)"
```

Copy and paste this into the `authorized_keys` file on your server.

## Configure cron job

This will sync the hosts information once a day at 9am:

```cron
0 9 * * * /etc/hosts.d/run-sync-hosts >/dev/null 2>&1
```

Still logged in as root, edit the crontab using `crontab -e` and add this line or a variant thereof.

## Licence

[MIT License][licence]

[licence]: LICENSE
