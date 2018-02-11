# SHEKEL - How to upgrade Masternode on single Mac Hot Wallet

> This is a community contributed guide. Feel free to suggest improvements via Issues or opening Pull Requests. Thank you!

**!!! This guide is for UPGRADING an existing SHEKEL Hot wallet MasterNode using the new Shekel ZeroCoin wallet and chain !!!**

**!!! See the [MasterNode Hot Qt Wallet + Cold Mac Setup Guide](guides/Masternode_Setup_Hot_Mac.md) for a new masternode !!!**

---

## Requirements
* Existing Shekel-qt wallet version 1.3.0.0 or higher on Mac already installed (if not, see the [MasterNode Hot Qt Wallet + Cold Mac Setup Guide](guides/Masternode_Setup_Hot_Mac.md) instead)
* Backup of your wallet.dat and Passphrase (in encrypted, which is recommended to do) on a seperate drive or folder
* Backup of your shekel.conf and masternode.conf (just in case you screw something up!)

---

## **Hot** Wallet Upgrade (Part 1) using the Qt GUI wallet on Mac


###        Backup your wallet! Copy your wallet.dat somewhere safe. Close down the wallet you want to upgrade
### i.     Download the newest SHEKEL-Qt.dmg wallet from https://github.com/shekeltechnologies/JewNew/releases/
#### ii.   Run SHEKEL-Qt.dmg from the Downloads folder. 
![Alt text](https://github.com/shekeltechnologies/Documentation/blob/master/images/shekel-mac-downloads.png "Downloads folder")
![Alt text](https://github.com/shekeltechnologies/Documentation/blob/master/images/shekel-mac-downloads2.png "Downloads folder 2")
#### iii.  You will see the following dialog box
![Alt text](https://github.com/shekeltechnologies/Documentation/blob/master/images/shekel-mac-application.png "Shekel Core Applications")
#### iv.   Drag the Shekel-Qt icon towards the Applications folder as shown by the black arrow, as below:
![Alt text](https://github.com/shekeltechnologies/Documentation/blob/master/images/shekel-mac-application-drag.png "Shekel Core Applications Drag")
#### v.     You will be prompted to replace the existing Shekel-Qt with the new one. Click Replace.
![Alt text](https://github.com/shekeltechnologies/Documentation/blob/master/images/shekel-mac-upgrade-replace.png "Shekel upgrade replace")
#### vi.    The applcations folder will pop up and the Shekel-qt icon will appear. Start the new Shekel-Qt wallet.
![Alt text](https://github.com/shekeltechnologies/Documentation/blob/master/images/shekel-mac-icon.png "Shekel-qt icon")
#### vii.   Depending on your MAC's current security settings one or more things might have happened. Either the wallet runs fine, in which case proceed to the next few steps, or you might get the following error and clicking the ? will get you the help guide next to it:
![Alt text](https://github.com/shekeltechnologies/Documentation/blob/master/images/shekel-mac-unidentified.png "Shekel-qt unidentified developer")
![Alt text](https://github.com/shekeltechnologies/Documentation/blob/master/images/shekel-mac-unidentified-override.png "Shekel-qt unidentified developer override")
#### viii.  The easiest way to get around this is to simply hold down Control (CTRL) on your keyboard and  click Shekel-qt. You will get a dialog box, with the option to 'Open' as the first option. Click open. Now, you might get another box warning you Shekel-Qt was downloaded from the Internet. Click Open.
![Alt text](https://github.com/shekeltechnologies/Documentation/blob/master/images/shekel-mac-unidentified-openanyway.png "Shekel-qt unidentified developer open")
![Alt text](https://github.com/shekeltechnologies/Documentation/blob/master/images/shekel-mac-unidentified-openanyway2.png "Shekel-qt unidentified developer open box")
#### ix.   The Shekel-Qt wallet will now open
![Alt text](https://github.com/shekeltechnologies/Documentation/blob/master/images/shekel-mac-wallet.png "Shekel-qt wallet")
Let the wallet sync until you see this symbol
![Alt text](https://github.com/shekeltechnologies/Documentation/blob/master/images/shekel-wallet-sync.png "Wallet Sync Completed")


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

You can close down the Mac Wallet and run the shekel-qt again to restart the wallet
Then rerun the `startmasternode` command again in the Mac wallet.

> Remember as this is a standalone Mac Hot Wallet that holds the collateral and runs the masterode it can NOT be closed without impacting the operation of the MasterNode in the network. You must let it run 24/7.

You should now be able to see your MasterNode(s) on this web page: [http://shekel.mn.zone](http://shekel.mn.zone).

If Port 5500 is not green, i.e it is red, then you have a port forward issue and you need to port forward from your router or you need to allow it through the Firewall

Cheers!
