# Multiverse-Stellar
https://medium.com/@pitchayasaksenachai/install-private-stellar-network-on-google-cloud-1b948ff340dd

Changelog
- Update READ ME
- Update  gcloud image  ubuntu-minimal-1910-eoan

1.  Create Service accounts with permission to access to Google Cloud Storage (1) https://console.cloud.google.com/iam-admin/serviceaccounts?project=${gcloud_project_id}&supportedpurview=project
2.  Create Cloud Storage bucket for history archive (2)
3.  Create Cloud Storage bucket for Deployment scripts


### Install Stellar Core Validator
$ cd testnet
$ cp config.ini.template config.ini
Edit config file with your parameters.
GCP_PROJEC_NAME:  # gcloud project id
HISTORY_ARCHIVE_ACCOUNT_NAME:  # service account name from Step  (1)
HISTORY_ARCHIVE:             # Bucket name  for  history archive  (2)
DEPLOYMENT_SCRIPTS:     # Bucket name  for  Deployment scripts  (3)

**   run linux  (MacOs  sed throws 'bad flag in substitute command'  ...)

```sh
$ ./build.sh
$ ./deploy.sh
```

NAME              TYPE                 STATE      ERRORS  INTENT
core-validator-1  compute.v1.instance  COMPLETED  []
core-validator-2  compute.v1.instance  COMPLETED  []
core-validator-3  compute.v1.instance  COMPLETED  []

NAME          TYPE                 STATE      ERRORS  INTENT
core-horizon  compute.v1.instance  COMPLETED  []

### Post installation
1. Check Stellar Core services running in normal states.
2. Edit startup scripts of all GCE instance
3.
 ```sh
#!/bin/bash
cd /etc/stellar
sudo -u stellar stellar-core --conf /etc/stellar/stellar-core.cfg force-scp
sudo chown -R stellar:stellar /opt/stellar
sleep 60s
sudo systemctl start stellar-core
```
