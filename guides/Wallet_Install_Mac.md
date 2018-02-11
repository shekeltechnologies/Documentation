# SHEKEL - How to set up SHEKEL Wallet on MacOS

> This is a community contributed guide. Feel free to suggest improvements via Issues or opening Pull Requests. Thank you!

**!!! This guide is for installing a new SHEKEL wallet using the new Shekel ZeroCoin wallet and chain !!!**

**!!! WARNING: Do not use this guide to run a masternode at home whether you have a static IP Address or not. Your IP Address can be traced back to your home, therefore it is unsafe. Always run the hot masternode wallet on a VPS or cloud. You can still run a cold wallet at home which you do not need to run 24/7 !!!**

---

## Requirements
* MacOS 10.9 or higher
* Port 5500 port forwarded from your router (this allows more peers on even just a wallet)
* Basic knowledge of MAC

---

## Wallet Setup - installing the Qt GUI wallet on MAC


### 1. Install and open the Shekel-Qt wallet on your machine.

#### i.    Download the newest SHEKEL-Qt.dmg wallet from https://github.com/shekeltechnologies/JewNew/releases/
#### ii.   Run SHEKEL-Qt.dmg from the Downloads folder. 
![Alt text](https://github.com/shekeltechnologies/Documentation/blob/master/images/shekel-mac-downloads.png "Downloads folder")
![Alt text](https://github.com/shekeltechnologies/Documentation/blob/master/images/shekel-mac-downloads2.png "Downloads folder 2")
#### iii.  You will see the following dialog box
![Alt text](https://github.com/shekeltechnologies/Documentation/blob/master/images/shekel-mac-application.png "Shekel Core Applications")
#### iv.   Drag the Shekel-Qt icon towards the Applications folder as shown by the black arrow, as below:
![Alt text](https://github.com/shekeltechnologies/Documentation/blob/master/images/shekel-mac-application-drag.png "Shekel Core Applications Drag")
#### v.    The applcations folder will pop up and the Shekel-qt icon will appear. Start the new Shekel-Qt wallet.
![Alt text](https://github.com/shekeltechnologies/Documentation/blob/master/images/shekel-mac-icon.png "Shekel-qt icon")
#### vi.   Depending on your MAC's current security settings one or more things might have happened. Either the wallet runs fine, in which case proceed to the next few steps, or you might get the following error and clicking the ? will get you the help guide next to it:
![Alt text](https://github.com/shekeltechnologies/Documentation/blob/master/images/shekel-mac-unidentified.png "Shekel-qt unidentified developer")
![Alt text](https://github.com/shekeltechnologies/Documentation/blob/master/images/shekel-mac-unidentified-override.png "Shekel-qt unidentified developer override")
#### vii.  The easiest way to get around this is to simply hold down Control (CTRL) on your keyboard and  click Shekel-qt. You will get a dialog box, with the option to 'Open' as the first option. Click open. Now, you might get another box warning you Shekel-Qt was downloaded from the Internet. Click Open.
![Alt text](https://github.com/shekeltechnologies/Documentation/blob/master/images/shekel-mac-unidentified-openanyway.png "Shekel-qt unidentified developer open")
![Alt text](https://github.com/shekeltechnologies/Documentation/blob/master/images/shekel-mac-unidentified-openanyway2.png "Shekel-qt unidentified developer open box")
#### viii. Before you see the wallet, you will see the following dialog box asking you to choose the Data directory. If you choose the default Data directory, the location for this directory is `~/Library/Application\ Support/Shekel/`. You would therefore use the Finder (Icon that has a face) to type in this path to find it. In this example, I will be choosing a Custom path as shown in the screenshot, my user is called `macuser` but yours will be different. The username depends on the username you are using on your Mac, so replace it with your own:
![Alt text](https://github.com/shekeltechnologies/Documentation/blob/master/images/shekel-mac-data-directory-box.png "Shekel-qt Custom Data Directory")
#### ix.   The Shekel-Qt wallet will now open
![Alt text](https://github.com/shekeltechnologies/Documentation/blob/master/images/shekel-mac-wallet.png "Shekel-qt wallet")
Let the wallet sync until you see this symbol
![Alt text](https://github.com/shekeltechnologies/Documentation/blob/master/images/shekel-wallet-sync.png "Wallet Sync Completed")
#### x.    You may have noticed by now that the wallet does not open the Wallet and Masternode config files from the Tools menu. This is because you need to choose a program that will open them first. Right click the finder, click `Go to folder` and enter the path of the Data directory you chose in step viii and click Ok.
![Alt text](https://github.com/shekeltechnologies/Documentation/blob/master/images/shekel-mac-data-directory-3.png "Shekel-qt wallet")
![Alt text](https://github.com/shekeltechnologies/Documentation/blob/master/images/shekel-mac-data-directory-4.png "Shekel-qt wallet")
#### xi.   You will now see the data directory for your wallet. Double click either `Shekel.conf` or `Masternode.conf` to open them and you will see this messsage. Click on `Choose Application` and select `TextEdit` from Applications, this will open one of the config files. Now, you will be able to open these directly from the Shekel-Qt wallet's Tools menu. You can then save your changes at the top by clicking `File > Save` for the steps in this guide.
![Alt text](https://github.com/shekeltechnologies/Documentation/blob/master/images/shekel-mac-data-directory-5.png "Shekel-qt wallet")
![Alt text](https://github.com/shekeltechnologies/Documentation/blob/master/images/shekel-mac-data-directory-6.png "Shekel-qt wallet")
![Alt text](https://github.com/shekeltechnologies/Documentation/blob/master/images/shekel-mac-data-directory-7.png "Shekel-qt wallet")
![Alt text](https://github.com/shekeltechnologies/Documentation/blob/master/images/shekel-mac-data-directory-8.png "Shekel-qt wallet")
![Alt text](https://github.com/shekeltechnologies/Documentation/blob/master/images/shekel-mac-data-directory-9.png "Shekel-qt wallet")
![Alt text](https://github.com/shekeltechnologies/Documentation/blob/master/images/shekel-mac-data-directory-10.png "Shekel-qt wallet")
![Alt text](https://github.com/shekeltechnologies/Documentation/blob/master/images/shekel-mac-data-directory-11.png "Shekel-qt wallet")
#### xii.  Encrypt your wallet with a long passphrase and either save it in a password manager such as keepass, or write it down and keep it safe (in a locked compartment or safe) (recommended). This passphrase is your only key to your wallet, do NOT lose it or you will lose all your JEWS. Do not let anyone steal your passcode or wallet either, just like in real life!
To encrypt the wallet, go to Settings > Encrypt wallet. Enter the passphrase, click ok. You will then have to restart the wallet and then go to Settings > Unlock Wallet and then enter the passphrase to unlock the wallet, for staking, controlling the masternode or sending your JEWS.
#### xiii. Back up your wallet.dat in case of a mistake as soon as you encrypt your wallet. Once you have encrypted the wallet, your previous backups will not work, so back it up by going to File > Backup Wallet and save the backup to more than one place. Such as a USB key or a network share. I recommend keeping your wallet and passphrase seperate so that no one can steal both. They would need both to do anything to your wallet or JEWS! You will find your wallet.dat in the same location as your Wallet and Masternode config files as in Steps viii to xi.

#### xiv.  If you ever minimize your wallet, you can find the icon in the Dock at the bottom right. Hold down Control (CTRL) and Click to get the menu options below:
![Alt text](https://github.com/shekeltechnologies/Documentation/blob/master/images/shekel-mac-dock2.png "Shekel-qt wallet")
![Alt text](https://github.com/shekeltechnologies/Documentation/blob/master/images/shekel-mac-dock.png "Shekel-qt wallet")
