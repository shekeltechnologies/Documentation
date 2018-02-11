# SHEKEL - How to set up Masternode on single Windows Hot Wallet

> This is a community contributed guide. Feel free to suggest improvements via Issues or opening Pull Requests. Thank you!

**!!! This guide is for installing a new SHEKEL Hot wallet MasterNode using the new Shekel ZeroCoin wallet and chain !!!**
**!!! WARNING: DO NOT ATTEMPT TO USE THIS WALLET TO UPGRADE FROM THE WHITE JEW WALLET (OLD JEW), YOU NEED TO SWAP BY 28th Feb, see the discord) !!!**


**!!! WARNING: Do not run a Windows masternode at home whether you have a static IP Address or not. Your IP Address can be traced back to your home, therefore it is unsafe. You can still run a cold wallet at home !!!**

---

## Requirements
* Windows 7, Server 2013 or higher running on a VPS or cloud
* Static IP Address
* Port 5500 port forwarded from your router
* Basic knowledge of Windows

---

## Wallet Setup(Part 1) installing the Qt GUI wallet on Windows

> The MasterNode requires a collateral of 25000 JEW coins which will have to be transferred and stored. You can buy these from the exchanges listed on the http://Shekel.io website.
> This will run 24/7 and provide services to the network via TCP port 5500 for which it will be rewarded with coins. 
> Since this is one wallet that holds your funds as well as running the masternode, you run the risk of losing the funds in the event of an attack.
> After the setup is complete, this wallet needs to have a stable Internet Connection and will need to run 24/7.

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
---

### 2. Create a receiving address for the Masternode collateral funds.

   Go to File -> Receiving addresses...
   
   Click **New**, type in a label and press **Ok**.
   
   ![Alt text](https://github.com/shekeltechnologies/Documentation/blob/master/images/shekel_new_address.png "Receiving Address")

### 3. Select the row of the newly added address and click **Copy** to store the destination address in the clipboard.
### 4. Send exactly 25000 JEW coins to the address you just copied. Double check you've got the correct address before transferring the funds.
     After sending, you can verify the balance in the Transactions tab. This can take a few minutes to be confirmed by the network.

### 5. Open the debug console of the wallet in order to type a few commands. 

   Go to `Tools` -> `Debug console`

### 6. Run the following command: `masternode genkey`

   ![Alt text](https://github.com/shekeltechnologies/Documentation/blob/master/images/shekel_console_genkey.png "Wallet Debug Console genkey")

 You should see a long key that looks like:
   ```
   3HaYBVUCYjEMeeH1Y4sBGLALQZE1Yc1K64xiqgX37tGBDQL8Xg
   ```
   We will use this later on.

### 7. Run `masternode outputs` command to retrieve the transaction ID of the collateral transfer.

   You should see an output that looks like this:
   ```
   [
      {
        "txhash" : "6782efab3a76fa557370ec3b9c13bf0d0df3d4df63adc018e1dd90e1c8da088e",
        "outputidx" : 1
      }
   ]
   ```

   Both `txhash` and `outputidx` will be used in the next step. `outputidx` can be `0` or `1`, both are valid values
   
---

**!!!For anyone having issues with masternode outputs being blank!!!**
>If you have given the transaction a few minutes to get a confirmation and you still do not get any output from masternode outputs it means that you have not sent EXACTLY 25000 JEW in a single transaction. 
>To fix this, you do not need to send coins back to the exchange. You can send yourself coins from within your wallet. It is good practice to use a separate address for each masternode so that you can see the rewards from each masternode in a different address.
>So, follow the steps below. You can change the MN01 to MN02 for your 2nd masternode, etc. In fact, you can give the address any label that makes sense to you!

>Go to `Tools` -> `Debug console`
```
getnewaddress MN01
```
>A new address will be output. Copy the address.
```
sendtoaddress copied-address 25000
```
>Wait 1 minute
```
masternode outputs
```
>Done.

---


### 8. Go to `Tools` -> `Open Masternode Configuration File` and add a line in the newly opened `masternode.conf` file.
> If you get prompted to choose a program, select notepad.exe to open it. 

> This is an example of what you need in masternode.conf. Ignore any example text that may already be in there that contains a '#' in front of each line, that is just an example to help you. Read it if it helps.
```
mn1 your_vps_ip_address:5500 your_masternode_key_output_from-masternode_genkey txhash_from-masternode_outputs Outputidx_from-masternode_outputs
```
> The file will contain an example that is commented out(with a # in front), but based on the above values, I would add this line in:
```
MN1 45.76.33.125:5500 3HaYBVUCYjEMeeH1Y4sBGLALQZE1Yc1K64xiqgX37tGBDQL8Xg 6782efab3a76fa557370ec3b9c13bf0d0df3d4df63adc018e1dd90e1c8da088e 1
```
>   Where `45.76.33.125` is the external IP of the masternode server that will provide services to the network.

>   Where `3HaYBVUCYjEMeeH1Y4sBGLALQZE1Yc1K64xiqgX37tGBDQL8Xg` is your masternode key from `masternode genkey`.

>   Where `6782efab3a76fa557370ec3b9c13bf0d0df3d4df63adc018e1dd90e1c8da088e` is your txhash from `masternode outputs`.

>   Where `1` is your outputidx from `masternode outputs`

### 9. Restart the Qt wallet to pick up the `masternode.conf` changes.
### 10. Go to Masternodes tab and check if your newly added masternode is listed.


> If you are running the Windows MasterNode server in Amazon AWS or another place where additional firewalls are in place, you need to allow incoming connections on port 5500/TCP


### 11. Edit the MasterNode main wallet configuration file:
```
Tools > Open Wallet Configuration File
```
> If you get prompted to choose a program, select notepad.exe to open it

Enter this wallet configuration data and change accordingly:
```
rpcuser=<alphanumeric_rpc_username>
rpcpassword=<alphanumeric_rpc_password>
rpcport=5501
listen=1
server=1
daemon=1
maxconnections=250
masternode=1
externalip=<ip_address_here>:5500
masternodeaddr=<ip_address_here>:5500
masternodeprivkey=<the_wallet_genkey_value_here>
```
Click File and Save in notepad

This is a real example, based on the `genkey` obtained in the Cold(Part 1) wallet section:
```
rpcuser=shekelrpcuser
rpcpassword=someSUPERsecurePASSWORD3746375620
rpcport=5501
listen=1
server=1
daemon=1
maxconnections=250
masternode=1
externalip=45.76.33.125:5500
masternodeaddr=45.76.33.125:5500
masternodeprivkey=3HaYBVUCYjEMeeH1Y4sBGLALQZE1Yc1K64xiqgX37tGBDQL8Xg
```
> The IP address(`45.76.33.125` in this example) will be different for you. 
> In a web browser you can visit www.whatismyip.com to get your External IP Address.

> Same goes for the `masternodeprivkey` value, you need the key returned by the `masternode genkey` command executed in the Windows wallet earlier (Part 1).

> The exact same key needs to be used for the masternode entry in the `masternode.conf` file of your Wallet(Part 1)

### 12. Re-start the Windows wallet by closing it down and then running shekel-qt.exe again

### 13. Wait until the wallet is synced with the blockchain network:
Either look at the icon in the bottom right until there is a Blue tick or go to Tools > Information > current block size
```
You can also go to Tools > Debug and type in getinfo
``` 
> Give it 30 mins now for this node to "get social" with the other nodes in the network. Once it peers up with a good number of other masternodes, the following activation steps should work fine.


## Enable the Masternode

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
