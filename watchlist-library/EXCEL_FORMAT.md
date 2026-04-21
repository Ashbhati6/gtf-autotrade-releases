# Excel To Watchlist JSON Format

Use these columns in Excel:

```text
symbol | securityId | exchangeSegment | label
```

Recommended:

- `symbol`: stock symbol, for example `SBIN`
- `securityId`: optional. Leave blank if symbol is available in `server/data/dhan-master.csv`
- `exchangeSegment`: use `NSE_EQ` for NSE stocks
- `label`: display name in app

For NSE Excel downloads, a `SYMBOL` column is enough. The converter maps it to Dhan `SECURITY_ID` from `server/data/dhan-master.csv`.

Convert CSV:

```powershell
npm run make:watchlist -- --input "C:\Users\USER\Desktop\NIFTYAUTO.csv" --name "NIFTY AUTO" --category "Sector"
```

Convert XLS/XLSX if Microsoft Excel is installed:

```powershell
powershell -ExecutionPolicy Bypass -File scripts\excel-watchlist-to-json.ps1 -InputFile "C:\Users\USER\Desktop\NIFTYAUTO_20260421_121911.xls" -Name "NIFTY AUTO" -Category "Sector"
```

If conversion fails, keep the generated CSV for checking:

```powershell
powershell -ExecutionPolicy Bypass -File scripts\excel-watchlist-to-json.ps1 -InputFile "C:\Users\USER\Desktop\NIFTYAUTO_20260421_121911.xls" -Name "NIFTY AUTO" -Category "Sector" -DebugCsv "C:\Users\USER\Desktop\NIFTYAUTO_debug.csv"
```

Output:

```text
watchlist-library/packs/nifty-auto.json
watchlist-library/index.json
```

Then publish:

```powershell
$env:GH_TOKEN="YOUR_TOKEN"
npm run publish:watchlists
```
