# SHEKEL - How to upgrade Masternode on single Windows Hot Wallet

> This is a community contributed guide. Feel free to suggest improvements via Issues or opening Pull Requests. Thank you!

**!!! This guide is for UPGRADING an existing SHEKEL Hot wallet MasterNode using the new Shekel ZeroCoin wallet and chain !!!**
**!!! WARNING: DO NOT ATTEMPT TO USE THIS WALLET TO UPGRADE FROM THE WHITE JEW WALLET (OLD JEW), YOU NEED TO SWAP BY 28th Feb, see the discord) !!!**


**!!! See the [MasterNode Hot Qt Wallet + Cold Windows Setup Guide](guides/Masternode_Setup_Hot_Windows.md) for a new masternode !!!**

---

## Requirements
* Existing Shekel-qt wallet version 1.3.0.0 or higher on Windows already installed (if not, see the [MasterNode Hot Qt Wallet + Cold Windows Setup Guide](guides/Masternode_Setup_Hot_Windows.md) instead)
* Backup of your wallet.dat and Passphrase (in encrypted, which is recommended to do) on a seperate drive or folder
* Backup of your shekel.conf and masternode.conf (just in case you screw something up!)

---

## **Hot** Wallet Upgrade (Part 1) using the Qt GUI wallet on Windows


### 1. Backup your wallet! Copy your wallet.dat somewhere safe. Close down the wallet you want to upgrade
### 2. Download the newest shekel-qt.zip wallet from https://github.com/shekeltechnologies/JewNew/releases/
### 3. Extract the shekel-qt.exe from shekel-qt.zip
### 4. Replace your OLD shekel-qt.exe with the new one
### 5. Start the new shelkel-qt.exe
### 6. Let the wallet sync

---

## Re-enable the Masternode

### 1. Open `Tools` > `Debug console`.

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

Give it a few minutes and got to the Debug console again and type in:
```
masternode list-conf
```

If you see status `ENABLED`, you've done it, congratulations. Go hug someone now :)
It will take a few hours until the first rewards start coming in.

Instead, if you get status `Masternode not found in the list of available masternodes`, you need a bit more patience. Distributed systems take a bit of time to reach consensus. Restarting the wallets and retrying the start has been reported to help by community members. 

You can close down the Windows Wallet and run the shekel-qt.exe again to restart the wallet
Then rerun the `startmasternode` command again in the Windows wallet.

> Remember as this is a standalone Windows Hot Wallet that holds the collateral and runs the masterode it can NOT be closed without impacting the operation of the MasterNode in the network. You must let it run 24/7.

You should now be able to see your MasterNode(s) on this web page: [http://shekel.mn.zone](http://shekel.mn.zone).

If Port 5500 is not green, i.e it is red, then you have a port forward issue and you need to port forward from your router or you need to allow it through Windows Firewall

Cheers!
