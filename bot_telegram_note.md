# Creare un bot Telegram per prendere note personali

Questo esempio mostra i passi principali per creare un **bot Telegram** che funzioni come un “blocco note personale”: quando sei al lavoro gli mandi messaggi e lui li conserva in una chat privata.

---

## 1. Creare il bot con BotFather
- Apri Telegram e cerca l’utente **@BotFather**.  
- Scrivi il comando `/start`.  
- Scrivi `/newbot` e segui le istruzioni: ti chiederà un nome e un “username” (che deve finire con *bot*, tipo `MioBloccoNoteBot`).  
- Alla fine ti darà un **token** (una lunga stringa di lettere e numeri). Questo serve per parlare con il bot tramite codice.

---

## 2. Preparare un piccolo script per inviare note

Sul tuo PC (Linux, Raspberry o simile) crei uno script semplice, ad esempio in **bash** con `curl`:

```bash
#!/bin/bash
TOKEN="IL_TUO_TOKEN"
CHAT_ID="IL_TUO_CHAT_ID"
MESSAGGIO="$*"

curl -s -X POST "https://api.telegram.org/bot$TOKEN/sendMessage" -d chat_id="$CHAT_ID" -d text="$MESSAGGIO"
```

Questo script prende il testo che scrivi e lo manda al tuo bot, che lo recapita a te stesso su Telegram.

---

## 3. Scoprire il tuo Chat ID

- Scrivi un messaggio qualsiasi al bot appena creato. Cercalo per nome tra le chat
- Poi vai su:  

```
https://api.telegram.org/botIL_TUO_TOKEN/getUpdates
```  

(apri nel browser)  

- Nella risposta JSON troverai il tuo `chat.id`. È quel numero che devi mettere nello script.

### Perché serve `getUpdates`?
Quando un utente scrive al bot, Telegram registra quell’evento (un “update”) e lo mette in una coda interna.  
Il metodo **getUpdates** serve a leggere questa coda: all’interno trovi tutte le informazioni sui messaggi ricevuti dal bot, compreso il `chat.id` che identifica in modo univoco la conversazione tra te e il bot.  
Senza questo passaggio, il bot non saprebbe “dove” inviarti i messaggi.

---

## 4. Usarlo come blocco note

- Rendi lo script eseguibile:

```bash
chmod +x note.sh
```

- Poi ogni volta che sei alla tua postazione di lavoro puoi scrivere:

```bash
./note.sh "Ricordati di preparare la lezione"
./note.sh "IP nuovo: $(curl -s ifconfig.me)"
```

E il bot ti invierà subito il messaggio su Telegram.

---

👉 In questo modo hai un **recipiente di note personali** che vive su Telegram, sempre accessibile anche dal telefono quando ti allontani dalla scrivania.
