# SHEKEL Windows wallet install guide

> This is a community contributed guide. Feel free to suggest improvements via Issues or opening Pull Requests. Thank you!

**!!! This guide is for setting up a new wallet using the new Shekel ZeroCoin wallet and chain !!!**
**!!! WARNING: DO NOT ATTEMPT TO USE THIS WALLET TO UPGRADE FROM THE WHITE JEW WALLET (OLD JEW), YOU NEED TO SWAP BY 28th Feb, see the discord) !!!**

!!! WARNING: Do not use this guide to run a masternode at home whether you have a static IP Address or not. Your IP Address can be traced back to your home, therefore it is unsafe. Always run the hot masternode wallet on a VPS or cloud. You can still run a cold wallet at home which you do not need to run 24/7 !!!

---

## Requirements
* Windows 7 or higher
* Static IP Address
* Port 5500 port forwarded from your router (this allows more peers on even just a wallet)
* Basic Windows skills

---

## Wallet Install using the Qt GUI wallet on Windows, OSX, etc

### 1. Install and open the Shekel-Qt wallet on your machine.

#### i.    Download the newest shekel-qt.zip wallet from https://github.com/shekeltechnologies/JewNew/releases/
#### ii.   Extract the shekel-qt.exe from shekel-qt.zip
#### iii.  Start the new shelkel-qt.exe
#### iv.   Click Run if you get this warning:
![Alt text](https://github.com/shekeltechnologies/Documentation/blob/master/images/shekel-windows-openfile.png "Wallet Open File Warning")
#### v.    If this is the first time you have started the wallet, you will be asked to enter a custom data directory. We recommend you enter the following, this creates the data directory where you extracted the shekel-qt.exe in part ii. It will be easier to find your wallet and config files if you know where they are:
![Alt text](https://github.com/shekeltechnologies/Documentation/blob/master/images/shekel-windows-data-directory-box.png "Wallet Data Directory box")
#### vi.   If this is the first time you have started the wallet, you will be asked to Allow Access by the firewall, click Allow access:
![Alt text](https://github.com/shekeltechnologies/Documentation/blob/master/images/shekel-windows-firewall.png "Wallet Windows Firewall Warning")
#### vii.  Let the wallet sync until you see this symbol
![Alt text](https://github.com/shekeltechnologies/Documentation/blob/master/images/shekel-wallet-sync.png "Wallet Sync Completed")

#### viii. Encrypt your wallet with a long passphrase and either save it in a password manager such as keepass, or write it down and keep it safe (in a locked compartment or safe) (recommended). This passphrase is your only key to your wallet, do NOT lose it or you will lose all your JEWS. Do not let anyone steal your passcode or wallet either, just like in real life!
To encrypt the wallet, go to Settings > Encrypt wallet. Enter the passphrase, click ok. You will then have to restart the wallet and then go to Settings > Unlock Wallet and then enter the passphrase to unlock the wallet, for staking, controlling the masternode or sending your JEWS.
#### ix.   Back up your wallet.dat in case of a mistake as soon as you encrypt your wallet. Once you have encrypted the wallet, your previous backups will not work, so back it up by going to File > Backup Wallet and save the backup to more than one place. Such as a USB key or a network share. I recommend keeping your wallet and passphrase seperate so that no one can steal both. They would need both to do anything to your wallet or JEWS!
