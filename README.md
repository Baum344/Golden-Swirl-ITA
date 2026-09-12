# Golden Swirl — Traduzione Italiana (fan-made)

Traduzione **non ufficiale** in italiano di *Golden Swirl* (build Windows, Unity 2022.3.62f2, Addressables 1.22.3).

> Questo pacchetto non contiene il gioco. Per usarlo devi possedere una copia di *Golden Swirl*.
> Tutti i diritti su gioco, testi, asset e codice appartengono a **Snako Production Limited**.
> Qui viene distribuito solo il lavoro di traduzione e le istruzioni/strumenti per applicarlo alla tua copia locale.

## Stato

- **4.086 stringhe** tradotte su 19 tabelle (`Buff`, `Event`, `Card`, `Relic`, `CommonString`, `Character`, …).
- **Italiano selezionabile** in *Opzioni → Lingua* (patch del menu, che era hardcoded nel codice).
- Nessuna modifica alla logica di gioco, nessuna dipendenza aggiornata, nessuna versione di Unity cambiata.
- Validazione token/markup: 3.980+ stringhe con set di token identico all'inglese; l'unica differenza è un testo letterale dentro un formatter `{Color:choose(...)}`, tradotto perché effettivamente mostrato al giocatore.

## Installazione

Requisiti: Windows, PowerShell 5.1+, la copia di *Golden Swirl*.

1. Apri PowerShell nella cartella di questo pacchetto.
2. Esegui:

   ```powershell
   .\apply-italian.ps1 -GameDir "C:\percorso\a\Golden Swirl"
   ```

   dove `GameDir` è la cartella che contiene `GoldenSwirl.exe` e `GoldenSwirl_Data`.
   Se hai copiato il pacchetto dentro la cartella del gioco, puoi omettere `-GameDir`.

Lo script salva un backup in `italian-backup-<data>` e copia i file tradotti.

3. Avvia il gioco → **Opzioni → Lingua → Italiano**.

Per verificare l'integrità:

```powershell
.\verify.ps1 -GameDir "C:\percorso\a\Golden Swirl"
```

### Installazione manuale

Copia il contenuto di `patch/overlay/` sopra la cartella del gioco (mantenendo la struttura):

```
GoldenSwirl_Data/Managed/Assembly-CSharp.dll
GoldenSwirl_Data/StreamingAssets/aa/catalog.json
GoldenSwirl_Data/StreamingAssets/aa/StandaloneWindows64/localization-string-tables-italian(it)_assets_all.bundle
GoldenSwirl_Data/StreamingAssets/aa/StandaloneWindows64/localization-asset-tables-italian(it)_assets_all.bundle
GoldenSwirl_Data/StreamingAssets/aa/StandaloneWindows64/localization-locales-italian(it)_assets_all.bundle
```

## Cosa contiene il pacchetto

```
translations/
  it_strings.json      Tutte le stringhe con id, chiave, inglese e italiano
  it_strings.csv       Le stesse stringhe in CSV (facile da revisionare)
  it_only.json         Solo le traduzioni (id -> italiano)
patch/
  overlay/             File pronti da copiare nella cartella del gioco
  overlay.sha256       Hash SHA-256 per la verifica
  scripts/             Strumenti (ricostruzione bundle/catalogo/patch DLL)
GLOSSARY.md            Glossario EN -> IT usato
QA_REPORT.md           Report di controllo qualità
apply-italian.ps1      Installer automatico
verify.ps1             Verifica integrità
```

## Come funziona (per chi vuole contribuire)

Il gioco usa **Unity Localization + Addressables**. La traduzione è composta da:

1. **Nuove tabelle stringa italiane** (19 `StringTable` + `AssetTable`) inserite in un bundle dedicato con identità interna univoca.
2. **Un `Locale` italiano** (`it`, nome visualizzato "Italiano (it)").
3. **Voci aggiunte al catalogo Addressables** (`<Tabella>_it`, `AssetTable_it`, `Italian (it)`, label `Locale-it`) mantenendo invariato il resto.
4. **Patch minimale di `Assembly-CSharp.dll`**: il menu della lingua aveva un dizionario hardcoded di 10 lingue; ho aggiunto `"Italiano" → "it"`. La patch è chirurgica (nuove stringhe nel heap `#US`, 4 istruzioni in `OptionsUIPanel::.cctor`, trasloco nello slack di `.text` del solo metodo `Init`).

Per ricostruire tutto dai file di traduzione, vedi `patch/scripts/`.

## Contribuire

- Modifica `translations/it_strings.csv` (o `it_strings.json`).
- Mantieni **inalterati** token `{...}`, tag `<...>`, placeholder e `\n`/`\r`/`\t`.
- Apri una Pull Request spiegando il contesto delle modifiche.

## Crediti e note legali

- Traduzione italiana: fan-made (aggiungi qui il tuo nome/handle).
- *Golden Swirl* © Snako Production Limited.
- Questo progetto non è affiliato né approvato da Snako Production.


<a href="https://www.buymeacoffee.com/Baum344" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png" alt="Buy Me a Coffee" style="height: 60px !important;width: 217px !important;" ></a>

Grazie per il supporto! ❤️
