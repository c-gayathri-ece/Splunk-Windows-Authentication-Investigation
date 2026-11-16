# Evidence

Sanitised screenshots from the Splunk investigation. Usernames other than lab accounts are shown as `[hidden]`. Figures were captured on 16 Nov 2026, except the three event-level views (05, 07, 08), which were captured on 14 Nov 2026 and show individual events.

| Screenshot | Shows |
|---|---|
| `01-event-counts-by-eventcode.png` | Event counts: 4624 = 282,773; 4672 = 62,981; 4625 = 2,074; no 4728/4732 |
| `02-failed-vs-successful-logons-by-account.png` | Failed vs successful logons per target account (0 successful for the accounts shown) |
| `03-hourly-failed-logons-chart.png` | Failed logons per hour, with the largest spike around 4 Nov |
| `04-repeated-failed-logons-5min-windows.png` | Five-minute windows with 5 or more failures (41 windows; largest 268) |
| `05-failed-logon-burst-22-20-to-22-25.png` | The 268 failed logons from 22:20 to 22:25 on 4 Nov (Logon Type 3 in the rows shown) |
| `06-special-privileges-4672-by-account-host.png` | 4672 counts by account and host (`Arcsight3` dominates) |
| `07-logon-4624-and-privilege-4672-correlation.png` | 4624 and 4672 events matched by Logon ID `0x1D735272B4` |
| `08-logon-4624-detail-logon-type-3.png` | The matching 4624 logon, Logon Type 3 |
