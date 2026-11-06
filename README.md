# EJECT ($EJECT) – "Out before the dev."

`index.html` är sajten (v2, session-layouten) med CSS och JS inbakade, plus `og.png` (X-förhandsvisning) och `fav.png` (favicon). Den klassiska termkit-versionen ligger kvar under `/v1`. Grafiken till X ligger i `grafik/`.

Vill du byta till v1 som huvudsajt: flytta `v1/index.html` till roten.

## Fyll i CONFIG (överst i scriptet i index.html)

| Fält | Vad |
|---|---|
| `ca` | $EJECT-CA när den finns. Tom = "posted here and on X at launch", köpknappen visar "live at launch". |
| `dev` | $EJECT-dev-wallet (valfritt). Används av "arm $EJECT" så holders kan bevaka er egen dev. Tom = hittas on-chain vid första traden. |
| `x` | Länk till X-kontot. |
| `rpcWs` / `rpcHttp` | Solanas publika RPC (gratis, utan nyckel). Lägg en gratis Helius-URL först i listan om trafiken växer. |
| `wallMints` | Hur många nya launches live-loggen bevakar samtidigt (24). |

## Vad som är riktigt och vad som är preview

- **Riktigt:** nya launches via PumpPortals gratisström (`subscribeNewToken`). Trades läses direkt från Solana med `logsSubscribe` och avkodas från pump.funs `TradeEvent` (dev, wallet, köp/sälj, belopp). Dev-wallet hittas on-chain. Larmet fungerar: ljud, notis, banner och delbart kort.
- **Preview:** själva auto-sellen. Larmet säger tydligt "auto-sell · preview … nothing was sold for you".
- PumpPortals `subscribeTokenTrade` och `subscribeAccountTrade` kostar numera (API-nyckel + 0.02 SOL). Därför går wallet-bevakningen via Solanas publika RPC i stället.
- Om live-flödena inte svarar inom 9 s kör live-loggen simulerad data, märkt "preview".

## Deploy

GitHub → Vercel, Framework: **Other**, ingen build, root = mappen med index.html.

## Kolla efter deploy

1. Typsnittet är JetBrains Mono (Google Fonts laddas på riktiga domänen).
2. X-förhandsvisning: klistra in länken i en tweet-draft och kolla att og.png syns.
3. Live-data: under "live" ska lampan bli **LIVE** och launches börja ticka in inom några sekunder. Arma en färsk launch och tryck "test the alarm".
