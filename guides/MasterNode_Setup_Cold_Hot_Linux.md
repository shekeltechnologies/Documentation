## SHEKEL Cold - Hot(Linux) wallet MasterNode setup guide

> This is a community contributed guide. Feel free to suggest improvements via Issues or opening Pull Requests. Thank you!

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

This is will run 24/7 and provide services to the network via TCP port 5500 for which it will be rewarded with coins. It will run with an empty wallet reducing the risk of loosing the funds in the event of an attack.

1. Get a VPS server from a provider like Vultr, DigitalOcean, Linode, Amazon AWS, etc. 

Requirements:
 * Linux VPS (Ubuntu, Debian or similar)
 * Static IPv4 Address
 * Recommended at least 1GB of RAM 
