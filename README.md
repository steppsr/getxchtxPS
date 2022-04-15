## XCH Transaction Exporter : getxchtx [Powershell Edition]

Generate a list of transactions for Chia (XCH) into a CSV file.

---

**getxchtxPS.ps1** - The script pulls all your transactions into a json file by Chia CLI commands, then loops through each transaction building a CSV file. 

---

```
Usage: chia wallet get_transactions [OPTIONS]

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
  -v, --verbose
  -h, --help       Show this message and exit.

Do not use -o or -l with any of the filter options (year, min, max, type).

Example:
     .\getxchtxPS -y 2021 -v

Example for saving to file:
     .\getxchtxPS -y 2021 >tx_list.csv

```

---

**Notes:**

1. You must use **Windows PowerShell** or **Windows PowerShell ISE** to execute the script.
2. You should not use -o (_offset_) or -l (_limit_) with any of the Filter options (_year_, _min_, _max_, _type_).
3. Since this is pulling historical transactions, the current price column is set to 0. You will need to populate that column manually.

---

Disclaimer: For educational purposes only.