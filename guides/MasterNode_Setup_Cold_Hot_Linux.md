# SHEKEL Cold + Hot wallet MasterNode setup guide

> This is a community contributed guide. Feel free to suggest improvements via Issues or opening Pull Requests. Thank you!

**!!! This guide is for setting up a new MasterNode using the new Shekel ZeroCoin wallet and chain !!!**
**!!! WARNING: DO NOT ATTEMPT TO USE THIS WALLET TO UPGRADE FROM THE WHITE JEW WALLET (OLD JEW), YOU NEED TO SWAP BY 28th Feb, see the discord) !!!**

**!!! WARNING: Do not run a Windows masternode at home whether you have a static IP Address or not. Your IP Address can be traced back to your home, therefore it is unsafe. You can still run a cold wallet at home !!!**

---

## Requirements
* Windows 7 or higher (This will be your Cold wallet)
* Ubuntu 14.04 or 16.04 running on a VPS such as Vultr, or other server (This will be your Hot wallet) running 24/7
* Static IP Address
* Port 5500 port forwarded from your router to your Ubuntu server
* Basic Linux skills

---

## **Cold** Wallet Setup(Part 1) using the Qt GUI wallet on Windows, OSX, etc

This is the wallet where the MasterNode collateral of 25000 JEW coins will have to be transferred and stored.
After the setup is complete, this wallet doesn't have to run 24/7 and will be the one receiving the rewards.

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
   We will use this later on both cold and hot wallets.

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

> This is an example of masternode.conf
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

>   Where `1` is your outputidx from `masternode outputs`.
      
### 9. Restart the Qt wallet to pick up the `masternode.conf` changes.
### 10. Go to Masternodes tab and check if your newly added masternode is listed.
> If you want to control multiple hot wallets from this cold wallet, you will need to repeat the previous 2-10 steps. The `masternode.conf` file will contain an entry for each masternode that will be added to the network.

At this point, we are going to configure our remote Masternode server.


------


## **Hot** MasterNode VPS Setup(Part 2) with Linux CLI only wallet

Requires details from (Part 1).

This will run 24/7 and provide services to the network via TCP port 5500 for which it will be rewarded with coins. It will run with an empty wallet reducing the risk of loosing the funds in the event of an attack.

### 1. Get a VPS server from a provider like Vultr, DigitalOcean, Linode, Amazon AWS, etc. 

Requirements:
 * Linux VPS (**Ubuntu 14.04** 64 bit and **Ubuntu 16.04** 64 bit) - Choose the correct version for your OS from the release page
 * Dedicated Public IP Address
 * Recommended at least 1GB of RAM 


### 2. Login via SSH into the server and type the following command in the console as root:

If you are using Windows, [PuTTY](https://putty.org) is a very good SSH client that you can use to connect to a remote Linux server.
If you are running a VPS from Vultr or similar, you need to use SSH such as putty if you want to copy and paste these commands otherwise you will have to type them all out!

Update and Install new packages by running these commands line by line *ONE* by *ONE*:

**!!!  Do not copy the entire thing and try to paste it, it will not work! Type or paste only one line at a time and hit enter after each line !!!**

```
apt-get update
apt-get upgrade -y
apt-get install wget nano unrar unzip libboost-all-dev libevent-dev software-properties-common -y
add-apt-repository ppa:bitcoin/bitcoin -y
apt-get update
apt-get install libdb4.8-dev libdb4.8++-dev -y
```

### 3. Configure swap to avoid running out of memory:

```
fallocate -l 1500M /mnt/1500MB.swap
dd if=/dev/zero of=/mnt/1500MB.swap bs=1024 count=1572864
mkswap /mnt/1500MB.swap
swapon /mnt/1500MB.swap
chmod 600 /mnt/1500MB.swap
echo '/mnt/1500MB.swap  none  swap  sw 0  0' >> /etc/fstab
```

### 4. Allow the MasterNode p2p communication port through the OS firewall:

```
ufw allow 22/tcp
ufw limit 22/tcp
ufw allow 5500/tcp
ufw logging on
```

If you are running the MasterNode server in Amazon AWS or another place where additional firewalls are in place, you need to allow incoming connections on port 5500/TCP



### 5. Install the Shekel CLI wallet. Always download the latest [release available](https://github.com/shekeltechnologies/JewNew/releases), unpack it

If you are already running a `shekeld` on your server and want to upgrade it, stop the current one with:
```
shekel-cli stop
```
Run the following command until the shekeld process disappears.
```
ps aux | grep shekeld | grep -v grep
```


For **Ubuntu 14.04**

```
apt-get install libzmq3 libminiupnpc-dev -y
wget https://github.com/shekeltechnologies/JewNew/releases/download/1.3.0.0/shekel-linux-1.3.0.zip
unzip shekel-linux-1.3.0.zip
rm shekel-linux-1.3.0.zip
chmod +x shekel-cli shekeld
mv shekel-cli shekeld /usr/local/bin/
shekeld
```

For **Ubuntu 16.04***

```
apt-get install libzmq3-dev libminiupnpc-dev -y
wget https://github.com/shekeltechnologies/JewNew/releases/download/1.3.0.0/shekel-Ubuntu16.04-1.3.0.zip
unzip shekel-Ubuntu16.04-1.3.0.zip
rm shekel-Ubuntu16.04-1.3.0.zip
chmod +x shekel-cli shekeld
mv shekel-cli shekeld /usr/local/bin/
cd ..
shekeld
```

You'll get a start error like `Error: To use shekeld, or the -server option to shekel-qt, you must set an rpcpassword in the configuration file`. It's expected because we haven't created the config file yet.

The service will only start for a second and create the initial data directory(`~/.shekel/`).

### 6. Edit the MasterNode main wallet configuration file:
```
nano /root/.shekel/shekel.conf
```

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
masternodeprivkey=<the_colw_wallet_genkey_value_here>
```
You can right click in SHH (putty) to paste all of the above

Exit the editor by CTRL+X and hit Y + ENTER to commit your changes.

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

The IP address(`45.76.33.125` in this example) will be different for you. Use the `ifconfig` command to find out your IP address, normally the address of the `eth0` interface.
Same goes for the `masternodeprivkey` value. You need the key returned by the `masternode genkey` command executed in the Cold Wallet(Part 1). The exact same key needs to be used for the masternode entry in the `masternode.conf` file of your Cold Wallet(Part 1)


### 7. Start the service with:
```
shekeld
```

### 8. Wait until is synced with the blockchain network:
Run this command every few mins until the block count stopped increasing fast.
```
shekel-cli getinfo
``` 
Give it 30 mins now for this node to "get social" with the other nodes in the network. Once it peers up with a good number of other masternodes, the following activation steps should work fine.


## Enable the Masternode

### 1. Go back to the local(cold) wallet and open `Tools` > `Debug console`.

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
ps aux | grep shekeld | grep -v grep
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
