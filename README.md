## XCH Transaction Exporter : getxchtx [Powershell Edition]

Generate a list of transactions for Chia (XCH) into a CSV file.

---

**getxchtxPS.ps1** - The script pulls all your transactions into a json file by Chia CLI commands, then loops through each transaction building a CSV file. 

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

**How to Get the Script**
You can just right-click on the **getxchtxPS.ps1** file and choose _Save link as..._ Save this file into a directory on your machine that you want to keep the script and the CSV file. I would suggest creating a new directory under Documents. 

**\*** If you download the full Zip file, you will need to extract the files first and store them in a directory.


**How to Open Powershell**
Type _powershell_ into the search box by the Windows Start button.
Right-click the Windows Powershell app and choose _Run as Administrator_
You need to change the directory to the location you have the script. Be sure to replace 'steve' with your username, and also '1.3.1' with your current version number.

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
In this example my fingerprint is **3812331296**, you will need to replace that with the fingerprint of your wallet. I also passed in the command option for just transactions from 2021 and use the **>** symbol and my filename to write the data into a file instead of to the screen. You can run it without the **> filename.csv** first to see what the output will look like.

```
.\getxchtxPS -f 3812331296 -y 2021 > chia_transactions_2021.csv
```

**Advanced Features**
You could use multiple command options to get a variety of different results. By default the script will use **wallet_id** of **1** which is the _STANDARD\_WALLET_. Passing in the **wallet_id** for a CAT wallet, will list the transactions for only that CAT wallet.

**Notes:**
1. You must run this script on the computer running the Farmer.
2. The **fingerprint** is required to run the script.
3. You must use **Windows PowerShell** or **Windows PowerShell ISE** to execute the script.
4. You should not use -o (_offset_) or -l (_limit_) with any of the Filter options (_year_, _min_, _max_, _type_).
5. Since this is pulling historical transactions, the current price column is set to 0. You will need to populate that column manually.

---
Disclaimer: For educational purposes only.

---
