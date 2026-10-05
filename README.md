# makej-app

Brigádnická appka (`/worker/`) a firemní dashboard (`/employer/`) pro
**app.makej.eu**. Statika, žádný build — JSX překládá Babel až v prohlížeči.

Marketingový web je zvlášť v [`makej-web`](https://github.com/Makej-sro/makej-web)
na `makej.eu`.

## Proč je to oddělené

Dřív bylo obojí v jednom repu a jednom nasazení, takže změna CSS na úvodce
přenasadila i dashboard a dva lidé si v jednom repu šlapali. Teď se nasazuje
každé zvlášť.

## Co musí zůstat shodné s makej-web

| soubor | proč |
|---|---|
| `pamet-prihlaseni.js` | drží přihlášení napříč oběma doménami — rozdílné verze = lidé se odhlašují |
| `cenik.css` | stejný vzhled ceníku na webu i v dashboardu |

U obou je to **vědomá kopie**, ne nedopatření. Když měníš jeden, zkontroluj druhý.

## Přihlášení napříč doménami

Session leží v cookie na `.makej.eu`, ne v `localStorage` — ten patří jednomu
původu a `makej.eu` s `app.makej.eu` by si ho nesdílely. Podrobnosti nahoře
v `pamet-prihlaseni.js`.

Nová adresa musí být povolená i v Supabase → Authentication → URL Configuration.

## Známé nedodělky

- `/right-arrow.png` a `/checked.png` — `employer-main.jsx` je načítá, ale
  v repu nikdy nebyly a vracely 404 i na původní adrese.
- `E_DEMO_INZERATY = true` v `employer-demo.jsx` — před spuštěním vypnout.
