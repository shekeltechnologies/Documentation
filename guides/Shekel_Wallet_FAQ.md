# SHEKEL Frequently Asked Questions

> This is a community contributed guide. Feel free to suggest improvements via Issues or opening Pull Requests. Thank you!

---

## Question 1:
>   My wallet will not stake, how can I fix this?
## Answer 1:
>   Go to `Tools` -> `Debug console`
>   Run `getstakingstatus`
>   Everything below should be set to true:
```      
getstakingstatus

{
    "validtime" : true,
    "haveconnections" : true,
    "walletunlocked" : true,
    "mintablecoins" : true,
    "enoughcoins" : true,
    "mnsync" : true,
    "staking status" : true
}
```
>   `haveconnections:` if false, you don't have connections to the coin network. Check for firewall and router to see if port 5500 is blocked outbound

>   `walletunlocked:` if false, go to `Settings > Unlock wallet` and enter your passphrase and check "For anonymous and staking only"

>   `mintablecoins:` if false, you either don't have any unlocked coins or they are not mature yet. Wait 1 hour

>   `mnsync:` if false, wait 20 minutes. If still false, try `mnsync reset` in the debug console and wait another 20 minutes

>   `staking status:` if false, resolve everything above. Go to `Settings > Options > Network` and check "Map port using uPnP. 
>
>   Edit shekel.conf, add line `staking=1`, save file. Close and reopen wallet. Wait 20 minutes.

---

## Question 2:
>   How can I check my masternode is working?
## Answer 2:
>   Check the following:

>   i.     On the Windows/Mac wallet's Masternodes tab;

>          -     The status field is ENABLED and the Active field is greater than 0:00

>   ii.    On the Windows/Mac wallet Go to `Tools > Debug console`

>          and type `masternode list-conf` check that everything looks ok, particularly `Status: ENABLED`  

>   iii.   On the Linux vps (via PUTTY SSH), if you have one:

>          Type `shekel-cli masternode status` and look for the message `Masternode successfully started`

>   iv.    Check http://shekel.mn.zone

>          Search for your masternode by IP Address or wallet address
>          Ensure that:
>          a. Port shows as 5500 and is green
>          b. Status is `ENABLED`
>          c. Wallet is `1.3.0` or higher (if on Windows, it's 1.2.1 or higher)
>          d. Active Time is > 0 and increases over time
>          e. Last seen is less than 1 hour.
>
>          If all these checks are successful, your masternode is working correctly. You may have to wait over 24 hours for your FIRST reward.

---

## Question 3:
>   Where is the default SHEKEL data directory on Mac?
## Answer 3:
>   Unless you changed it the default directory is:
   ```~/Library/Application\ Support/Shekel/```

---

## Question 4:
>   Where is the default SHEKEL data directory on Windows?
## Answer 4:
>   Unless you changed it the default directory is:
   ```%APPDATA%\Shekel```
