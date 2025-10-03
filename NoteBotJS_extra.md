# Bot Telegram minimale in JavaScript (Node.js)

Esempio essenziale per inviare un messaggio a un **bot Telegram** usando **JavaScript** su **Node.js** senza librerie esterne.  
Usiamo la `fetch` **nativa di Node 18+** (nessuna dipendenza).

> Se hai una versione di Node più vecchia, aggiorna a 18+ per avere `fetch` nativa. (Per semplicità non usiamo pacchetti aggiuntivi.)

---

## Codice `noteBot.js`

```js
// Richiede Node 18+ (fetch nativa)
const token  = "IL_TUO_TOKEN";
const chatId = "IL_TUO_CHAT_ID";
const msg    = "Ciao dal bot JavaScript!";

const url = "https://api.telegram.org/bot" + token + "/sendMessage"
          + "?chat_id=" + encodeURIComponent(chatId)
          + "&text="    + encodeURIComponent(msg);

(async () => {
  try {
    const res = await fetch(url);
    const data = await res.json();
    console.log(data);
  } catch (err) {
    console.error("Errore nella richiesta:", err);
  }
})();
```

---

## Come funziona

1. Inserisci il tuo **token** (dato da [BotFather](https://core.telegram.org/bots#botfather)) e il tuo **chatId**.  
2. Ottieni il `chat_id`: scrivi un messaggio al tuo bot e poi apri nel browser:  
   ```
   https://api.telegram.org/botIL_TUO_TOKEN/getUpdates
   ```
   Nella risposta JSON troverai `message.chat.id`.
3. Salva il file come `noteBot.js`.  
4. Esegui lo script con Node:  
   ```bash
   node noteBot.js
   ```
5. Dovresti ricevere il messaggio su Telegram dal tuo bot.

---

## Perché usare `getUpdates` per il `chat_id`
Quando l’utente scrive al bot, Telegram registra un *update* (evento) in una coda.  
Il metodo **`getUpdates`** serve a leggere quella coda: dentro ogni evento di messaggio c’è l’oggetto `chat` con l’`id` della conversazione. È questo numero che il bot deve usare come `chat_id` per inviarti i messaggi.
