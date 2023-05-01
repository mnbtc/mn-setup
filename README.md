
# mnbtc Masternode Setup Guide
***
## Required
1) **mnbtc collatera: 2000 MNBTC
2) **Local Wallet https://github.com/mnbtc/mnbtc/releases**
3) **VPS with UBUNTU 18.04** (it is possible to work on other versions but it is not tested)
4) **Putty https://www.putty.org/**
5) **Text editor on your local pc to save data for copy/paste**
***

***On your Local Wallet***
* Create an address with a label MN1 and send exactly the collateral amount to it. Wait to complete 6 confirmations on “ Payment to yourself “ created.

* Open the Debug Console ( Tools – Debug Console ) and type ***createmasternodekey***.
You will then receive your private key, save it in a txt to use it later.
  ```
 Example:
      createmasternodekey    
      
 Output should be: 
          6yvU9ECYz1SmW3yLhRxwEqA1eHN2s2bUQZZ4vLr1XsGj8s3bHYG   ```
	  
	  
* Still at Debug Console type ***getmasternodeoutputs*** and save txhash and outputidx on a txt
  ```
  Example:
          "txhash" : "12fce79c1a5623aa5b5830abff1a9feb6a682b75ee9fe22c647725a3gef42saa",
		         "outputidx" : 0   ```

***On Putty***

1. * Once logged in your vps, *copy/paste* each line one by one with *Enter*

```
wget https://raw.githubusercontent.com/mnbtc/mn-setup/master/masternodesetup.sh
```
2. With this command you will make masternode-install.sh executable:  

- Use this: <br>
```
sudo chmod +x masternodesetup.sh
``` <br>

3. Now install your masternode.  
```
./masternodesetup.sh
```



* Let this run, and when it ask you to install dependencies, if you're not sure press ***y*** and then enter

* It will take some time and then will ask to compile the Daemon, press ***y*** and then enter 

* Last thing script will ask you is to provide Masternode Genkey. Copy the one you got previously (createmasternodekey) and press enter.

Remember to do `mnbtc-cli getblockcount` to check if VPS catching blocks till it synced with chain, if not follow this procedure:

* Go to your wallet-qt and check peers list (tools - peers list) and select one ip from the list. With that ip do the follow command at VPS `mnbtc-cli addnode "ip" onetry`

      Example:
		  mnbtc-cli addnode 45.32.144.158 onetry
    
* Check now if VPS already downloading blocks with the command `mnbtc-cli getblockcount`, and if yes give it time now to catch last block number 

Do not close your terminal/ command prompt window at this point.

***Go back to your Local Wallet***

* Open the Masternode Configuration file (tools – open masternode configuration file) and add a new line (without #) using this template (bold needs to be changed) in the final save it and close the editor

**ALIAS VPS_IP**:15224 **masternodeprivkey TXhash Output**

		Example:
		MN1 125.67.32.10:15224 6yvU9ECYz1SmW3yLhRxwEqA1eHN2s2bUQZZ4vLr1XsGj8s3bHYG 12fce79c1a5623aa5b5830abff1a9feb6a682b75ee9fe22c647725a3gef42saa 0

* Close and Re-open Local Wallet, and at Masternode Tab you will find your MN with status MISSING

***(For the next steps you need to have already 16 confirmation on “Payment to yourself “ created in first step)***

* Go to Debug Console type the following: ***startmasternode alias 0 (mymnalias)***

		Example:
		startmasternode alias 0 MN1
***

***Go back to Putty***

```
mnbtc-cli getmasternodestatus
```

You need to get **"status" : 4** 

## Congratulations your mnbtc node it's running
