## XCH Transaction Exporter : getxchtx [Powershell Edition]

Generate a list of transactions for Chia (XCH) into a CSV file.

---

**getxchtxPS.ps1** - The script pulls all your transactions into a json file by Chia CLI commands, then loops through each transaction building a CSV file. 

---

**How to Get the Script**

You can just right-click on the **getxchtxPS.ps1** file and choose _Save link as..._ Save this file into a directory on your machine that you want to keep the script and the CSV file. I would suggest creating a new directory under Documents. 

**\*** If you download the full Zip file, you will need to extract the files first and store them in a directory.


**How to Open Powershell**

Type _powershell_ into the search box by the Windows Start button.
Right-click the Windows Powershell app and choose _Run as Administrator_
You need to change the directory to the location you have the script. Be sure to replace **steve** with your username, and also **1.3.1** with your current version number.

```
cd C:\Users\steve\AppData\Local\chia-blockchain\app-1.3.1\resources\app.asar.unpacked\daemon
```

**Do you know your fingerprint?**

You will need the fingerprint of your wallet. If you don't know the fingerprint you can run the following command:

```
chia keys show
```
**Now change to the script directory**

Now to run the script, you will need change to the directory where you saved the file.

```
cd C:\Users\Steve\Documents\Chia\getxchtxPS
```

**And finally, run the script**

In this example my fingerprint is **3812331296**, you will need to replace that with the fingerprint of your wallet. I also passed in the command option for just transactions from 2021 and used the **>** symbol and my filename to write the data into a file instead of to the screen. You can run it without the **> filename.csv** first to see what the output will look like.

```
.\getxchtxPS -f 3812331296 -y 2021 > chia_transactions_2021.csv
```

**Advanced Features**

You could use multiple command options to get a variety of different results. By default the script will use **wallet_id** of **1** which is the _STANDARD\_WALLET_. Passing in the **wallet_id** for a CAT wallet, will list the transactions for only that CAT wallet.

If you want to run the script for more than one **wallet_id** and have all the transactions in one file, you should replace the **>** with **>>** on each run **after** the first one. The first should always be **>** because that start a new empty file. **>>* is how you _append_ to an existing file instead of creating a new one.

For example, if I wanted to get all the transactions in both my STANDARD_WALLET and the wallet for the Chia Holiday 2021 Token which is in **wallet_id** number **2** for me, then I would run these commands.

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
0x84ec3be356271402070c8c72ad8fb299783c9f9c7ae321b127aa090fc50f320c,04/14/2022 21:15:27,FEE_REWARD,0.25,0
0xd6199a6c6935dc170c573129cbe4527800807e8712d51118aa40e670cc43dc96,04/14/2022 20:43:27,FEE_REWARD,0.25,0
0xcb6e50c106a16498edb0f85fe8d4d2e26e2edf4f15a906af1345cda6c5a83798,04/14/2022 20:42:52,FEE_REWARD,0.25,0
0xdff0766926c97bf2cfc238d14418458d452af47acb1ab8e3016b7035766c7af9,04/14/2022 20:40:40,FEE_REWARD,0.25,0
0x735a475096e93485fa857b302b4a8cec203794c3f841c6daa34c45d7ebec5e27,04/13/2022 10:29:38,OUTGOING_TX,0.000000000001,0
0x643308a2707d8c14a1bbbebe774cb9aef379f4f937217481da0c5d80a42b7ecb,04/12/2022 20:20:42,OUTGOING_TX,0.00000000001,0
0x3b07a7c330c16020c582f589ab1f6b2e6833b09d92035d835e402fe0696e8cb4,03/31/2022 20:42:28,INCOMING_TX,1,0
```

Below is an example of the output in Verbose mode:

```
0x84ec3be356271402070c8c72ad8fb299783c9f9c7ae321b127aa090fc50f320c,04/14/2022 21:15:27,FEE_REWARD,0.25,0,@{amount=250000000000; parent_coin_info=0xfc0af20d20c4b3e92ef2a48bd291ccb2
000000000000000000000000000cc218; puzzle_hash=0xec9d7c3abef4cb992e272c3faaf1514138218eeefd947fec37208c5e810d85b2},True,836124,0,,,0,,none,,0xec9d7c3abef4cb992e272c3faaf1514138218e
eefd947fec37208c5e810d85b2,none,1
0xd6199a6c6935dc170c573129cbe4527800807e8712d51118aa40e670cc43dc96,04/14/2022 20:43:27,FEE_REWARD,0.25,0,@{amount=250000000000; parent_coin_info=0xfc0af20d20c4b3e92ef2a48bd291ccb2
000000000000000000000000000cc1a0; puzzle_hash=0xec9d7c3abef4cb992e272c3faaf1514138218eeefd947fec37208c5e810d85b2},True,836003,0,,,0,,none,,0xec9d7c3abef4cb992e272c3faaf1514138218e
eefd947fec37208c5e810d85b2,none,1
0xcb6e50c106a16498edb0f85fe8d4d2e26e2edf4f15a906af1345cda6c5a83798,04/14/2022 20:42:52,FEE_REWARD,0.25,0,@{amount=250000000000; parent_coin_info=0xfc0af20d20c4b3e92ef2a48bd291ccb2
000000000000000000000000000cc19f; puzzle_hash=0xec9d7c3abef4cb992e272c3faaf1514138218eeefd947fec37208c5e810d85b2},True,836001,0,,,0,,none,,0xec9d7c3abef4cb992e272c3faaf1514138218e
eefd947fec37208c5e810d85b2,none,1
0xdff0766926c97bf2cfc238d14418458d452af47acb1ab8e3016b7035766c7af9,04/14/2022 20:40:40,FEE_REWARD,0.25,0,@{amount=250000000000; parent_coin_info=0xfc0af20d20c4b3e92ef2a48bd291ccb2
000000000000000000000000000cc19a; puzzle_hash=0xec9d7c3abef4cb992e272c3faaf1514138218eeefd947fec37208c5e810d85b2},True,835996,0,,,0,,none,,0xec9d7c3abef4cb992e272c3faaf1514138218e
eefd947fec37208c5e810d85b2,none,1
0x735a475096e93485fa857b302b4a8cec203794c3f841c6daa34c45d7ebec5e27,04/13/2022 10:29:38,OUTGOING_TX,0.000000000001,0,@{amount=1; parent_coin_info=0xc49aefc4fb0bf8c5fd61d3cfceb2d7a1
ac226791891b3321edded1479cc31954; puzzle_hash=0xeff07522495060c066f66f32acc2a77e3a3e737aca8baea4d1a64ea4cdc13da9}@{amount=999999999788; parent_coin_info=0xc49aefc4fb0bf8c5fd61d3cf
ceb2d7a1ac226791891b3321edded1479cc31954; puzzle_hash=0x8342111338168ec0e7a224409079131225d12e5ee5b1903c280481f4b9990d0a}@{amount=1; parent_coin_info=0x9dbdbe6b40e0a467ac515f23d4a
c85e3ccdcefe41d9644e96e1f918d02725090; puzzle_hash=0x27a9356a5a7b9c9bd1306d7ddd33ca4159ee5b6db38f1ad1985ee2d6cb935581},True,829842,0.000000000001,, ,1,8ef74c0d7d602955027425fa4921
378c0cd71ab9c31f8f82e60bddb726a84432 3 NO_TRANSACTIONS_WHILE_SYNCING,@{aggregated_signature=0xa6804e6aba70625a50f8323c99dd8e1b7edd1078b110e6fe8da3fd53c83e94def828585ca0bd14c26f4a1
9e7b41034ab186127a0f41fad265c27eb288e3fb550e43bc0581138b453727bdd2003cd3625efe3f67dd3c40aac858aafd3aa32343f; coin_spends=System.Object[]},,0x27a9356a5a7b9c9bd1306d7ddd33ca4159ee5b
6db38f1ad1985ee2d6cb935581,none,1
0x643308a2707d8c14a1bbbebe774cb9aef379f4f937217481da0c5d80a42b7ecb,04/12/2022 20:20:42,OUTGOING_TX,0.00000000001,0,@{amount=10; parent_coin_info=0x3b07a7c330c16020c582f589ab1f6b2e
6833b09d92035d835e402fe0696e8cb4; puzzle_hash=0xec9d7c3abef4cb992e272c3faaf1514138218eeefd947fec37208c5e810d85b2}@{amount=999999999790; parent_coin_info=0x3b07a7c330c16020c582f589
ab1f6b2e6833b09d92035d835e402fe0696e8cb4; puzzle_hash=0x005c1be39099bc84903231a4a74e9fdb5ba54adfc9b971e874604ed923cbab64},True,827113,0.0000000002,0x8457a52308c198c8ea1dbfc1c501cc
36e5442e1af02d8f172d8bdb4002c611b3 System.Object[],,2,8ef74c0d7d602955027425fa4921378c0cd71ab9c31f8f82e60bddb726a84432 3 NO_TRANSACTIONS_WHILE_SYNCINGf6edf3bf9faa987f521c2cca67dec
59fed0d31e3fd9009785ba1fab2b0a7f2c0 3 DOUBLE_SPEND,@{aggregated_signature=0xa8ca27b095c03498ac37ef488d5fff1e471f8767cb2d02878ac5db29feae87a8994f33be7186e5e9189d830a6162debc0973af6
154c95a541102d0aab6b02ce324e347bb7eafb0163ecacf699be522b27430420c3fc2b0851ea5d5e089845e70; coin_spends=System.Object[]},,0xec9d7c3abef4cb992e272c3faaf1514138218eeefd947fec37208c5e
810d85b2,none,1
0x3b07a7c330c16020c582f589ab1f6b2e6833b09d92035d835e402fe0696e8cb4,03/31/2022 20:42:28,INCOMING_TX,1,0,@{amount=1000000000000; parent_coin_info=0x3881d0ab5e7f57a48242ff5578b65c470
44fb836403feba4a63092e01622aa99; puzzle_hash=0xec9d7c3abef4cb992e272c3faaf1514138218eeefd947fec37208c5e810d85b2},True,771573,0,,,0,,none,,0xec9d7c3abef4cb992e272c3faaf1514138218ee
efd947fec37208c5e810d85b2,none,1
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
