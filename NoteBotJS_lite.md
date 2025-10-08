# Bot Telegram minimale in JavaScript (Node.js, versione semplificata)

Questo esempio mostra come inviare un messaggio a un **bot Telegram** usando **JavaScript** con Node.js.  
Usiamo la funzione `fetch` nativa (presente in Node 18+), ma senza `async/await`: sfruttiamo la sintassi con `.then()` che è più semplice da leggere per chi inizia.

---

## Codice `noteBot.js` (lato server con Node.js)

```js
const token  = "IL_TUO_TOKEN";
const chatId = "IL_TUO_CHAT_ID";
const msg    = "Ciao dal bot JavaScript!";

const url = "https://api.telegram.org/bot" + token + "/sendMessage"
          + "?chat_id=" + encodeURIComponent(chatId)
          + "&text="    + encodeURIComponent(msg);

fetch(url)
  .then(res => res.json())         // converte la risposta in JSON
  .then(data => console.log(data)) // stampa la risposta
  .catch(err => console.error("Errore:", err));
```

---

## Come funziona

1. Salva il file come `noteBot.js`.  
2. Esegui lo script con Node:  
   ```bash
   node noteBot.js
   ```
3. Se tutto è corretto, riceverai un messaggio su Telegram dal tuo bot.

---

## Lato server vs lato client

- **Server (Node.js, PHP, Java, Python, …)**  
  ✅ Sicuro: il token resta nascosto sul server.  
  ✅ È il metodo usato normalmente per gestire bot reali.

- **Client (Browser, JavaScript in HTML)**  
  Possibile usare `fetch()` direttamente in una pagina web, ma ⚠️ **non sicuro**:  
  il token del bot sarebbe visibile a chiunque apra il sorgente della pagina.  
  Per questo si evita e si preferisce sempre gestire le chiamate dal server.

---

