# builds.antderosa.com on the VPS

Plain HTML. nginx serves the checkout; a deploy is just the git update.

## Install (once, as root)

1. DNS: add an A record for `builds` → 177.7.44.106 (antderosa.com DNS).
2. Clone and install:

```bash
git clone https://github.com/soupsoup/ai-builds-showcase /var/www/builds
/var/www/builds/deploy/vps/install.sh
```


3. First deploy, then HTTPS:

```bash
systemctl start builds-deploy && systemctl enable --now builds-deploy.timer
journalctl -u builds-deploy -n 20 --no-pager
certbot --nginx -d builds.antderosa.com
```

After that, every push to main deploys within a minute. Roll back with
`sudo -u builds /var/www/builds/deploy/vps/deploy.sh --rollback <sha>`.
