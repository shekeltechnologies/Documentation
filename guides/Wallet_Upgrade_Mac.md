# SHEKEL - How to upgrade Masternode on single Mac Hot Wallet

> This is a community contributed guide. Feel free to suggest improvements via Issues or opening Pull Requests. Thank you!

**!!! This guide is for UPGRADING an existing SHEKEL wallet MasterNode using the new Shekel ZeroCoin wallet and chain !!!**
**!!! WARNING: DO NOT ATTEMPT TO USE THIS WALLET TO UPGRADE FROM THE WHITE JEW WALLET (OLD JEW), YOU NEED TO SWAP BY 28th Feb, see the discord) !!!**


**!!! See the [SHEKEL MAC Qt Wallet Install Guide](guides/Wallet_Install_Mac.md) for a new wallet!!!**

---

## Requirements
* Existing Shekel-qt wallet version 1.3.0.0 or higher on Mac already installed (if not, see the [SHEKEL MAC Qt Wallet Install Guide](guides/Wallet_Install_Mac.md) instead)
* Backup of your wallet.dat and Passphrase (in encrypted, which is recommended to do) on a seperate drive or folder
* Backup of your shekel.conf and masternode.conf (just in case you screw something up!)

---

## Wallet Upgrade using the Qt GUI wallet on Mac


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
