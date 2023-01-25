# Leto.gg(gateway.leto.gg) 

> A caching layer built for the leto metrics engine(this repo currently is using the configuration built by NFT.Storage)

This repo was originally written by the team at NFT.Storage. Big thanks to them for making this project possible!

## Getting started

    This is a simple AWS EC2 Server running a Kubo node configured to act as a IPFS gateway. I totally understand there are much better configurations to set a gateway up with but this is really just a testbed for some features in development and this is a good "vanilla" enviroment for me to test on. 

    1. Be sure to enable IPFS to run on this EC2 node by enabling an service. Do this by creating a new service file for IPFS by running the command sudo nano /etc/systemd/system/ipfs.service

    2. Then add the contents within "runtime/ipfs.service" into the file using NANO or VIM. 

   Extra Notes: 
   
- Reload the systemd configuration by running the command sudo systemctl daemon-reload

    - Enable the IPFS service to start automatically at boot by running the command sudo systemctl enable ipfs

    - Start the IPFS service by running the command sudo systemctl start ipfs

    - To check the status of the service, you can use the command sudo systemctl status ipfs

    - To stop the service, you can use the command sudo systemctl stop ipfs

## Bad-Bits Denylist Script for automated removal

    #!/bin/bash

    # specify the path to the default IPFS storage directory
    IPFS_STORAGE_DIR="~/.ipfs"

    # specify the deny-list file containing the CIDs of the files to be removed
    DENY_LIST_FILE="deny-list.json"

    # read the deny-list file
    CIDS=$(jq -r '.[]' $DENY_LIST_FILE)

    # loop through the CIDs in the deny-list file
    for CID in $CIDS; do
    # run the ipfs pin rm command to remove each CID
    ipfs pin rm $CID
    
- NOTE: Script Accessibility(you need to make sure the script can read the bad-bits file in regards to the filesystem the bad-bits.json file. 
done

