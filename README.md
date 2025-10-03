# send-telegram.sh

Questo script permette di inviare messaggi a un bot Telegram utilizzando le API ufficiali.

## Requisiti
- Un bot Telegram già creato con [@BotFather](https://t.me/BotFather).
- Il token del bot (`BOT_TOKEN`) e il `CHAT_ID` del destinatario (utente o gruppo).

## Installazione
1. Copia lo script in una directory, ad esempio:
   ```bash
   /usr/local/bin/send-telegram.sh
   ```
2. Modifica lo script inserendo i tuoi dati reali:
   ```bash
   BOT_TOKEN="INSERISCI_IL_TUO_TOKEN"
   CHAT_ID="INSERISCI_IL_TUO_CHAT_ID"
   ```
3. Rendi eseguibile il file:
   ```bash
   chmod +x /usr/local/bin/send-telegram.sh
   ```

## Utilizzo

### Messaggio predefinito
Se non passi nessun argomento, lo script invierà un messaggio di default:
```bash
./send-telegram.sh
```

### Messaggio personalizzato
Puoi specificare un messaggio personalizzato come argomento:
```bash
./send-telegram.sh "Nuovo IP pubblico: 203.0.113.7"
```

Oppure con più parole e spazi:
```bash
./send-telegram.sh "Server down! Riavvio necessario."
```

## Esempio di output
Se lo script è configurato correttamente, riceverai su Telegram un messaggio inviato dal tuo bot con il testo scelto.

---
