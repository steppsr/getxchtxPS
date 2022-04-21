## XCH Transaction Exporter : getxchtx [Powershell Edition]

Generate a list of transactions for Chia (XCH) into a CSV file.

---

**getxchtxPS.ps1** - The script pulls all your transactions into a json file by Chia CLI commands, then loops through each transaction building a CSV file. 

---

**How to Get the Script.**
You can just right-click on the **getxchtxPS.ps1** file and choose _Save link as..._ Save this file into a directory on your machine that you want to keep the script and the CSV file. I would suggest creating a new directory under Documents. 

**\*** If you download the full Zip file, you will need to extract the files first and store them in a directory.


**How to Open Powershell.**
Type _powershell_ into the search box by the Windows Start button.
Right-click the Windows Powershell app and choose _Run as Administrator_
You need to change the directory to the location you have the script. 
You should be able to copy/paste each line as is:

```
$appfolder=Get-ChildItem $ENV:LOCALAPPDATA\chia-blockchain -Directory -Filter "app*" | Sort-Object -Property Name -Descending | Select-Object -First 1
$path="$ENV:LOCALAPPDATA\chia-blockchain\" + $appfolder.Name + "\resources\app.asar.unpacked\daemon"
cd $path
```

**Change your Execution Policy for Powershell.** You may need to change the ExecutionPolicy for Powershell so it will allow you to run a script.

```
C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe -NoProfile -NoLogo -NonInteractive -ExecutionPolicy Bypass
```

**Do you know your fingerprint?**
You will need the fingerprint of your wallet. If you don't know the fingerprint you can run the following command:

```
.\chia keys show
```
**Now change to the script directory.**
Now to run the script, you will need change to the directory where you saved the file.

```
cd C:\Users\Steve\Documents\Chia\getxchtxPS
```

**And finally, run the script.**
In this example my fingerprint is **3812331296**, you will need to replace that with the fingerprint of your wallet. I also passed in the command option for just transactions from 2021 and used the **>** symbol and my filename to write the data into a file instead of to the screen. You can run it without the **> filename.csv** first to see what the output will look like.

```
.\getxchtxPS -f 3812331296 -y 2021 > chia_transactions_2021.csv
```

**Advanced Features.**
You could use multiple command options to get a variety of different results. By default the script will use **wallet_id** of **1** which is the _STANDARD\_WALLET_. Passing in the **wallet_id** for a CAT wallet, will list the transactions for only that CAT wallet.

If you want to run the script for more than one **wallet_id** and have all the transactions in one file, you should replace the **>** with **>>** on each run **after** the first one. The first should always be **>** because that start a new empty file. **>>* is how you _append_ to an existing file instead of creating a new one.

For example, if I wanted to get all the transactions in both my STANDARD_WALLET and the wallet for the Chia Holiday 2021 Token which is in **wallet_id** number **2** for me, then I would run these commands.

A recent Advanced Feature added is the -j command option that will allow you to specify the filename to save the output to in ASCII format.
```
.\getxchtxPS -f 3812331296 -i 1 > chia_transactions.csv
.\getxchtxPS -f 3812331296 -i 2 >> chia_transactions.csv
```

---

```
Usage: .\getxchtxPS [OPTIONS]

Options:
  -f INTEGER       Set the fingerprint to specify which wallet to use  [required]
  -i INTEGER       Id of the wallet to use                             [default: 1; required]
  -j FILENAME      Output to ASCII file instead of screen              [default: none]
  -o INTEGER       Skip transactions from the beginning of the list    [default: 0; required]
  -l INTEGER       Max number of transactions to return                [default: 4294967295]
  -y YEAR          Filter transactions to given 4-digit year (or all)  [default: all]
  -min XCH         Filter to transactions greater than XCH given       [default: 0]
  -max XCH         Filter to transactions less than XCH given          [default: 999999]
  -t INTEGER       Filter by transaction type                          [default: -1]
                          -1 All transaction types
                           0 INCOMING_TX
                           1 OUTGOING_TX
                           2 COINBASE_REWARD
                           3 FEE_REWARD
                           4 INCOMING_TRADE
                           5 OUTGOING_TRADE
  -v               Verbose output
  -h, --help       Show this message and exit

Do not use -o or -l with any of the filter options (year, min, max, type).

Example:
     .\getxchtxPS -y 2021 -f 3812331296 -v

Example for saving to file:
     .\getxchtxPS -y 2021 -f 3812331296 >tx_list.csv

```

---

Below is a sample of the output in normal mode (without the Verbose option):

```
fingerprint,tx_name,tx_datetime,tx_type,tx_amount,current_price,tx_fee_amount
3812331296,0x016672871817ce424d059d5f9814036a7928941c386eca2efdac22faed39f40f,04/16/2022 19:08:41,FEE_REWARD,0.25,0,0
3812331296,0xd5218c73522bc85c45bd7584b4fc012c1c354612ef4481358319dcfe871f89c8,04/16/2022 18:45:12,FEE_REWARD,0.25,0,0
3812331296,0x4c67fcd39f40e925927f767e0034b49fa1cd101b87ddedaa4c7a692abf636211,04/16/2022 18:43:00,FEE_REWARD,0.25,0,0
3812331296,0xc330f0492efb655f45f5dd877bda9c9e2cf71b55065082d0cd39056476dd45c0,04/16/2022 18:39:53,FEE_REWARD,0.25,0,0
3812331296,0x2c55094551c4692d70f1a1736c0f1ec4b796b4139196738e390acc83d644f501,04/16/2022 18:39:53,FEE_REWARD,0.25,0,0
3812331296,0xf24e07f506e8c9f4b57c7b334ec4c22be9d73934913a43e4a0dcdf409525988c,04/16/2022 18:13:37,FEE_REWARD,0.25,0,0
3812331296,0x5478659950f732b2b3b3198474a3715785456c887a862fccb44a9fa15f4b593b,04/16/2022 18:11:16,FEE_REWARD,0.25,0,0
3812331296,0xf1db488d334823f73983da1f0777a8990bb5a5f51b152559db8a03c2e6ec4f65,04/16/2022 18:04:58,FEE_REWARD,0.25,0,0
```

Below is an example of the output in Verbose mode:

```
fingerprint,tx_name,tx_datetime,tx_type,tx_amount,current_price,tx_fee_amount,tx_created_at_time,tx_addition
s,tx_confirmed,tx_confirmed_at_height,tx_memos,tx_removals,tx_sent,tx_sent_to,tx_spend_bundle,tx_to_address,tx_to_puzzle_hash,tx_trade_id,tx_wallet_id
3812331296,0xb264aa0df6d6591ec9b4499c06ff6f63f01e2f1054fd662185552fe952627a95,04/16/2022 20:33:35,FEE_REWARD,0.25,0,0,1650159215,@{amount=250000000000; parent_coin_info=0xfc0af20d20c4b3e92ef2a48bd291ccb2000000000000000000000000000ce59a; puzzle_hash=0xec9d7c3abef4cb992e272c3faaf1514138218eeefd947fec37208c5e810d85b2},True,845215,,,0,,none,,0xec9d7c3abef4cb992e272c3faaf1514138218eeefd947fec37208c5e810d85b2,none,1
3812331296,0x061e1f070cd0c3e0e5dac198f67a2482e2d687fccdbf5692884aef1e658d759e,04/16/2022 20:00:09,FEE_REWARD,0.25,0,0,1650157209,@{amount=250000000000; parent_coin_info=0xfc0af20d20c4b3e92ef2a48bd291ccb2000000000000000000000000000ce536; puzzle_hash=0xec9d7c3abef4cb992e272c3faaf1514138218eeefd947fec37208c5e810d85b2},True,845115,,,0,,none,,0xec9d7c3abef4cb992e272c3faaf1514138218eeefd947fec37208c5e810d85b2,none,1
3812331296,0x016672871817ce424d059d5f9814036a7928941c386eca2efdac22faed39f40f,04/16/2022 19:08:41,FEE_REWARD,0.25,0,0,1650154121,@{amount=250000000000; parent_coin_info=0xfc0af20d20c4b3e92ef2a48bd291ccb2000000000000000000000000000ce497; puzzle_hash=0xec9d7c3abef4cb992e272c3faaf1514138218eeefd947fec37208c5e810d85b2},True,844952,,,0,,none,,0xec9d7c3abef4cb992e272c3faaf1514138218eeefd947fec37208c5e810d85b2,none,1
3812331296,0xd5218c73522bc85c45bd7584b4fc012c1c354612ef4481358319dcfe871f89c8,04/16/2022 18:45:12,FEE_REWARD,0.25,0,0,1650152712,@{amount=250000000000; parent_coin_info=0xfc0af20d20c4b3e92ef2a48bd291ccb2000000000000000000000000000ce459; puzzle_hash=0xec9d7c3abef4cb992e272c3faaf1514138218eeefd947fec37208c5e810d85b2},True,844892,,,0,,none,,0xec9d7c3abef4cb992e272c3faaf1514138218eeefd947fec37208c5e810d85b2,none,1
3812331296,0x4c67fcd39f40e925927f767e0034b49fa1cd101b87ddedaa4c7a692abf636211,04/16/2022 18:43:00,FEE_REWARD,0.25,0,0,1650152580,@{amount=250000000000; parent_coin_info=0xfc0af20d20c4b3e92ef2a48bd291ccb2000000000000000000000000000ce458; puzzle_hash=0xec9d7c3abef4cb992e272c3faaf1514138218eeefd947fec37208c5e810d85b2},True,844890,,,0,,none,,0xec9d7c3abef4cb992e272c3faaf1514138218eeefd947fec37208c5e810d85b2,none,1
3812331296,0xc330f0492efb655f45f5dd877bda9c9e2cf71b55065082d0cd39056476dd45c0,04/16/2022 18:39:53,FEE_REWARD,0.25,0,0,1650152393,@{amount=250000000000; parent_coin_info=0xfc0af20d20c4b3e92ef2a48bd291ccb2000000000000000000000000000ce44e; puzzle_hash=0xec9d7c3abef4cb992e272c3faaf1514138218eeefd947fec37208c5e810d85b2},True,844882,,,0,,none,,0xec9d7c3abef4cb992e272c3faaf1514138218eeefd947fec37208c5e810d85b2,none,1
3812331296,0x2c55094551c4692d70f1a1736c0f1ec4b796b4139196738e390acc83d644f501,04/16/2022 18:39:53,FEE_REWARD,0.25,0,0,1650152393,@{amount=250000000000; parent_coin_info=0xfc0af20d20c4b3e92ef2a48bd291ccb2000000000000000000000000000ce44d; puzzle_hash=0xec9d7c3abef4cb992e272c3faaf1514138218eeefd947fec37208c5e810d85b2},True,844882,,,0,,none,,0xec9d7c3abef4cb992e272c3faaf1514138218eeefd947fec37208c5e810d85b2,none,1
3812331296,0xf24e07f506e8c9f4b57c7b334ec4c22be9d73934913a43e4a0dcdf409525988c,04/16/2022 18:13:37,FEE_REWARD,0.25,0,0,1650150817,@{amount=250000000000; parent_coin_info=0xfc0af20d20c4b3e92ef2a48bd291ccb2000000000000000000000000000ce403; puzzle_hash=0xec9d7c3abef4cb992e272c3faaf1514138218eeefd947fec37208c5e810d85b2},True,844807,,,0,,none,,0xec9d7c3abef4cb992e272c3faaf1514138218eeefd947fec37208c5e810d85b2,none,1
```

---

**Notes:**
1. You must run this script on the computer running the Farmer.
2. The **fingerprint** is required to run the script.
3. You must use **Windows PowerShell** or **Windows PowerShell ISE** to execute the script.
4. You should not use -o (_offset_) or -l (_limit_) with any of the Filter options (_year_, _min_, _max_, _type_).
5. Since this is pulling historical transactions, the current price column is set to 0. You will need to populate that column manually.

---
Disclaimer: For educational purposes only.

---
