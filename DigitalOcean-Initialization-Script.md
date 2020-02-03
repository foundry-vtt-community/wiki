[DigitalOcean](https://digitalocean.com) is a reasonably priced VM hosting provider, with their cheapest tier starting at $5/month. DigitalOcean has the added benefit of having setup scripts to simplify new spinups.

These instructions have been verified against an Ubuntu 18.04.3 droplet.

To run an init script, check the "User Data" box under "Select additional options", then paste in your desired script.

### For full hands-off deploy-and-go
Pros: Easy!

Cons: Hard to update / monitor

**For this script, you'll need to replace `__ACCESSKEY__` with a value from a Patreon release page, and __PORT__ with your desired port - use `80` if you want the easiest use**

```yaml
#cloud-config

packages:
  - unzip
  - nodejs

runcmd:
  - printf '\nSetting up server for Foundry VTT\n'
  - mkdir foundrycore
  - mkdir foundrydata
  - cd /foundrycore
  - wget https://foundryvtt.s3-us-west-2.amazonaws.com/releases/__ACCESSKEY__/FoundryVirtualTabletop-linux-x64.zip
  - unzip FoundryVirtualTabletop-linux-x64.zip
  - screen -S Foundry
  - printf '\nStarting up Foundry\n'
  - node /resources/app/main.js --port=__PORT__ --dataPath=/foundrydata/
```

Wait a few minutes, then verify Foundry started up by running `tail -100 /var/log/cloud-init-output.log`

### For just minimum dependencies
Pros: More control

Cons: You'll need to ssh in to finish setup
```yaml
#cloud-config

packages:
  - unzip
  - nodejs

runcmd:
  - printf '\nSetting up server for Foundry VTT\n'
  - mkdir foundrycore
  - mkdir foundrydata
```

#### Finishing setup

DigitalOcean will email you a one-time password to SSH in that you'll have to immediately change before executing further commands.

1. `ssh root@<Your Droplet IP>`
2. `cd /foundrycore`
3. `wget https://foundryvtt.s3-us-west-2.amazonaws.com/releases/<Patreon Access Key>/FoundryVirtualTabletop-linux-x64.zip`
4. `unzip FoundryVirtualTabletop-linux-x64.zip`
5. `screen -S Foundry` (creates a named background "screen" so the server stays running)
6. `node resources/app/main.js --port=<Desired Port> --dataPath=/foundrydata/`
7. `CTRL + A + D` (detach from screen)

If you ever want to reattach to the Screen, use `screen -r`
