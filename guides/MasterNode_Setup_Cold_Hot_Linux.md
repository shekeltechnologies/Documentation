## SHEKEL Cold - Hot(Linux) wallet MasterNode setup guide

> This is a community contributed guide. Feel free to suggest improvements via Issues or opening Pull Requests. Thank you!


**!!! This guide is for setting up a MasterNode using the new Shekel ZeroCoin wallet and chain !!!**


### **Cold** Wallet Setup(Part 1)

This is the wallet where the MasterNode collateral of 25000 JEW coins will have to be transferred and stored.
After the setup is complete, this wallet doesn't have to run 24/7 and will be the one receiving the rewards.

1. Install and open the Shekel-Qt wallet on your machine.

2. Create a receiving address for the Masternode collateral funds.

   Go to File -> Receiving addresses...
   
   Click **New**, type in a label and press **Ok**.
   
   ![Alt text](https://github.com/shekeltechnologies/Documentation/blob/master/images/shekel_new_address.png "Receiving Address")

3. Select the row of the newly added address and click **Copy** to store the destination address in the clipboard.
4. Send exactly 25000 JEW coins to the address you just copied. Double check you've got the correct address before transferring the funds.
5. After sending, you can verify the balance in the Transactions tab. This can take a few minutes to be confirmed by the network.
6. Open the debug console of the wallet in order to type a few commands. 

   Go to `Tools` -> `Debug console`

7. Run the following command: `masternode genkey`

   ![Alt text](https://github.com/shekeltechnologies/Documentation/blob/master/images/shekel_console_genkey.png "Wallet Debug Console genkey")

 You should see a long key that looks like:
   ```
   3HaYBVUCYjEMeeH1Y4sBGLALQZE1Yc1K64xiqgX37tGBDQL8Xg
   ```
   We will use this later on both cold and hot wallets.

8. Run `masternode outputs` command to retrieve the transaction ID of the collateral transfer.

   You should see an output that looks like this:
   ```
   [
      {
        "txhash" : "6782efab3a76fa557370ec3b9c13bf0d0df3d4df63adc018e1dd90e1c8da088e",
        "outputidx" : 1
      }
   ]
   ```

   Both `txhash` and `outputidx` will be used in the next step.

9. Go to `Tools` -> `Open Masternode Configuration File` and add a line in the newly opened `masternode.conf` file. The file will contain an example that is commented out, but based on the above values, I would add this line in:
   ```
   MN1 45.76.33.125:5500 3HaYBVUCYjEMeeH1Y4sBGLALQZE1Yc1K64xiqgX37tGBDQL8Xg 6782efab3a76fa557370ec3b9c13bf0d0df3d4df63adc018e1dd90e1c8da088e 1
   ```
   Where `45.76.33.125` is the external IP of the masternode server that will provide services to the network.
   
   If you want to control multiple hot wallets from this cold wallet, you will need to repeat the previous 2-10 steps. The `masternode.conf` file will contain an entry for each masternode that will be added to the network.

10. Restart the wallet to pick up the `masternode.conf` changes.
11. Go to Masternodes tab and check if your newly added masternode is listed.

At this point, we are going to configure our remote Masternode server.


------


## **Hot** MasterNode VPS Setup(Part 2)

Requires details from (Part 1).

This is will run 24/7 and provide services to the network via TCP port 5500 for which it will be rewarded with coins. It will run with an empty wallet reducing the risk of loosing the funds in the event of an attack.

1. Get a VPS server from a provider like Vultr, DigitalOcean, Linode, Amazon AWS, etc. 

Requirements:
 * Linux VPS (Ubuntu 14.04, 64 bit)
 * Static IPv4 Address
 * Recommended at least 1GB of RAM 


2. SSH into the server and:

Update and Install new packages (as user `root`) by running these commands one by one and ensuring success:
```
apt-get update -y
apt-get upgrade -y
apt-get install wget nano unrar unzip -y
apt-get install libboost-all-dev libevent-dev software-properties-common -y
add-apt-repository ppa:bitcoin/bitcoin -y
apt-get update
apt-get install libdb4.8-dev libdb4.8++-dev -y
```

3. Configure swap to avoid running out of memory:
```
fallocate -l 1500M /mnt/1500MB.swap
dd if=/dev/zero of=/mnt/1500MB.swap bs=1024 count=1572864
mkswap /mnt/1500MB.swap
swapon /mnt/1500MB.swap
chmod 600 /mnt/1500MB.swap
echo '/mnt/1500MB.swap  none  swap  sw 0  0' >> /etc/fstab
```

4. Allow the MasterNode p2p communication port through the OS firewall:
```
ufw allow 5500/tcp
ufw logging on
ufw --force enable
```

If you are running the MasterNode server in Amazon AWS or another place where additional firewalls are in place, you need to allow incoming connections on port 5500/tcp

5. Create a regular user and switch to in in order to run the wallet:
```
adduser mnguru
su mnguru
cd ~
```

For security reasons, do not run the MasterNode wallet under the superuser `root`.

6. Install Shekel (as user `mnguru`). Always download the latest [release available](https://github.com/shekeltechnologies/JewNew/releases), unpack it
```
wget https://github.com/shekeltechnologies/JewNew/releases/download/1.2.1.0/Shekel-linux.rar
unrar x Shekel-linux.rar
rm Shekel-linux.rar
chmod +x shekel-cli shekeld
./shekeld
```
You'll get a start error like `Error: To use shekeld, or the -server option to shekel-qt, you must set an rpcpassword in the configuration file`. It's expected because we haven't created the config file yet.

The service will only start for a second and create the initial data directory(~/.shekel/).

7. Edit the MasterNode main wallet configuration file:
nano ~/.shekel/shekel.conf

Enter this data and change accordingly:
```
rpcuser=<alphanumeric_rpc_username>
rpcpassword=<alphanumeric_rpc_password>
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
Exit the editor by CTRL+X and hit Y to commit your changes.

The IP address(`45.76.33.125` in this example) will be different for you. Use the `ifconfig` command to find out your IP address, normally the address of the `eth0` interface.
Same goes for the `masternodeprivkey` value. You need the key returned by the `masternode genkey` command executed in the Cold Wallet(Part 1). The exact same key needs to be used for the masternode entry in the `masternode.conf` file of your Cold Wallet(Part 1)


8. Start the service with:
```
./shekeld
```

9. Wait until is synced with the blockchain network:
Run this command every few mins until the block count stopped increasing fast.
```
./shekel-cli getinfo
``` 



## Enable the Masternode

1. Go back to the local(cold) wallet and open `Tools` > `Debug console`.

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


## Verify that the MasterNode is enabled and contributing to the network.

Give it a few minutes and go to the Linux VPS console() and check the status of the masternode with this command:
```
./shekel-cli masternode status
```

If you see status `Masternode successfully started`, you are golden, go hug someone.
It will take a few hours until the first rewards start coming in.

The masternode debug log (~/.shekel/debug.log) should also contain this line on a successful activation:
```
2018-02-02 02:07:12 CActiveMasternode::EnableHotColdMasterNode() - Enabled! You may shut down the cold daemon.
```

As the log entry says, your MasterNode is up and running and the hot wallet that holds the collateral can be closed without impacting the operation of the MasterNode in the network.

Cheers !
