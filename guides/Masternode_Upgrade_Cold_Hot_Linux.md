# SHEKEL MasterNode Hot Qt Wallet + Cold Linux Upgrade Guide

> This is a community contributed guide. Feel free to suggest improvements via Issues or opening Pull Requests. Thank you!

**!!! This guide is for upgrading an existing SHEKEL COLD & Hot wallet MasterNode using the new Shekel ZeroCoin wallet and chain !!!**

**!!! See the [MasterNode Hot Qt Wallet + Cold Linux Setup Guide](guides/MasterNode_Setup_Cold_Hot_Linux.md) for a new masternode !!!**

---

## Requirements
* Existing version of Shekel-qt on Windows v1.3.0.0 or higher already installed (if not, see the [MasterNode Hot Qt Wallet + Cold Linux Setup Guide](guides/MasterNode_Setup_Cold_Hot_Linux.md) instead)
* Existing version of shekeld and shekel-cli v1.3.0.0 or higher already installed on your Ubuntu 14.04/16.04 VPS
* Backup of your wallet.dat and Passphrase (in encrypted, which is recommended to do) on a seperate drive or folder
* Backup of your shekel.conf and masternode.conf (just in case you screw something up!)

---

## **Cold** Wallet Upgrade (Part 1) using the Qt GUI wallet on Windows, OSX, etc


### 1. Backup your wallet! Copy your wallet.dat somewhere safe. Close down the wallet you want to upgrade
### 2. Download the newest shekel-qt.zip wallet from https://github.com/shekeltechnologies/JewNew/releases/
### 3. Extract the shekel-qt.exe from shekel-qt.zip
### 4. Replace your OLD shekel-qt.exe with the new one
### 5. Start the new shelkel-qt.exe
### 6. Let the wallet sync

---

## **Hot** MasterNode VPS Upgrade(Part 2) with Linux CLI only wallet


## Requirements:
 * Linux VPS (**Ubuntu 14.04** 64 bit or **Ubuntu 16.04** 64 bit). Choose the correct version for your OS from the release page
 * Backup of your shekel.conf (just in case you screw something up!)

### 1. Login via SSH into the server and type the following command in the console as root:

If you are using Windows, [PuTTY](https://putty.org) is a very good SSH client that you can use to connect to a remote Linux server.

### 2. Stop the service with:
```
shekel-cli stop
```
Run the following command until the shekeld process disappears.
```
ps aux | grep shekeld
```


### 3. Upgrade the Shekel CLI wallet. Always download the latest [release available](https://github.com/shekeltechnologies/JewNew/releases), unpack it
#### For Ubuntu 14.04 (see below for 16.04)
**!!!  Do not copy the entire thing and try to paste it, it will not work! Type or paste only one line at a time and hit enter after each line **!!!
```
apt-get update -y
apt-get upgrade -y
apt-get install libzmq3 libminiupnpc-dev -y
wget https://github.com/shekeltechnologies/JewNew/releases/download/1.3.0.0/shekel-linux-1.3.0.zip
unzip shekel-linux-1.3.0.zip
rm shekel-linux-1.3.0.zip
chmod +x shekel-cli shekeld
mv shekel-cli shekeld /usr/local/bin/
```
#### For Ubuntu 16.04 only
**!!!  Do not copy the entire thing and try to paste it, it will not work! Type or paste only one line at a time and hit enter after each line **!!!
```
apt-get update -y
apt-get upgrade -y
apt-get install libzmq3-dev libminiupnpc-dev -y
wget https://github.com/shekeltechnologies/JewNew/releases/download/1.3.0.0/shekel-Ubuntu16.04-1.3.0.zip
unzip shekel-Ubuntu16.04-1.3.0.zip
rm shekel-Ubuntu16.04-1.3.0.zip
chmod +x shekel-cli shekeld
mv shekel-cli shekeld /usr/local/bin/
```

### 4. Start the service with:
```
shekeld
```

### 8. Wait until is synced with the blockchain network:
Run this command every few mins until the block count stopped increasing fast.
```
shekel-cli getinfo
``` 
Give it 30 mins now for this node to "get social" with the other nodes in the network. Once it peers up with a good number of other masternodes, the following activation steps should work fine.


## Re-Enable the Masternode

### 1. Go back to the local(cold) wallet and open `Tools` > `Debug console`.
#### ** Note, you might have to unlock the wallet first if you have a passphrase ***
Type this command to see all the MasterNodes loaded from the `masternode.conf` file with their current status:
```
masternode list-conf
```

You should now see the newly added MasterNode with a status of `MISSING`.

Run the following command, in order to enable it:
```
startmasternode alias false MN1
```
In this ^ case, the alias of my MasterNode was MN1, in your case, it might be different.


### 2. Verify that the MasterNode is enabled and contributing to the network.

Give it a few minutes and go to the Linux VPS console and check the status of the masternode with this command:
```
shekel-cli masternode status
```

If you see status `Masternode successfully started`, you've done it, congratulations. Go hug someone now :)
It will take a few hours until the first rewards start coming in.

Instead, if you get status `Masternode not found in the list of available masternodes`, you need a bit more patience. Distributed systems take a bit of time to reach consensus. Restarting the wallets and retrying the start has been reported to help by community members. This is how you restart the Linux wallet from the CLI:
```
shekel-cli stop
```
Run the following command until the shekeld process disappears.
```
ps aux | grep shekeld
```
Then run the daemon.
```
shekeld
```
Rerun the `startmasternode` command again in the Qt (Cold) wallet.

The masternode debug log (`/root/.shekel/debug.log`) will contain this line on a successful activation:
```
2018-02-02 02:07:12 CActiveMasternode::EnableHotColdMasterNode() - Enabled! You may shut down the cold daemon.
```
You can watch the log as it's being written by using this command:
```
tail -f /root/.shekel/debug.log
```
Stop watching the log by pressing CTRL+C

As the log entry says, your MasterNode is up and running and the hot wallet that holds the collateral can be closed without impacting the operation of the MasterNode in the network.

You should now be able to see your MasterNode(s) on this web page: [http://shekel.mn.zone](http://shekel.mn.zone)

Cheers !
