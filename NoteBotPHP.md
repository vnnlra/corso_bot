# Bot Telegram minimale in PHP

Questo esempio mostra come inviare un messaggio a un **bot Telegram** usando PHP in modo molto semplice, senza librerie esterne.  
Per ora **non usiamo cURL** (che vedremo più avanti quando tratteremo *testing* e *API REST*), ma solo `file_get_contents()`.

---

## Codice `noteBot.php`

```php
<?php
$token  = "IL_TUO_TOKEN";
$chatId = "IL_TUO_CHAT_ID";
$msg    = "Ciao dal bot PHP!";

$url = "https://api.telegram.org/bot" . $token . "/sendMessage"
     . "?chat_id=" . urlencode($chatId)
     . "&text="    . urlencode($msg);

// Invia la richiesta HTTP a Telegram
$response = file_get_contents($url);

// Stampa la risposta ricevuta (in formato JSON)
echo $response;
```
> Nota: questo approccio richiede che `allow_url_fopen` sia abilitato in `php.ini`.

---

## Come funziona

1. Inserisci il tuo **token** (dato da [BotFather](https://core.telegram.org/bots#botfather)) e il tuo **chatId**.  
2. Ottieni il `chat_id`: scrivi un messaggio al tuo bot e poi apri nel browser:  
   ```
   https://api.telegram.org/botIL_TUO_TOKEN/getUpdates
   ```
   Nella risposta JSON troverai `message.chat.id`.
3. Salva il file come `noteBot.php`.  
4. Esegui lo script da terminale o mettilo su un server PHP:  
   ```bash
   php noteBot.php
   ```
5. Se tutto è corretto, riceverai un messaggio su Telegram dal tuo bot.

---

## Perché usare `getUpdates` per il `chat_id`
Quando l’utente scrive al bot, Telegram registra un *update* (evento) in una coda.  
Il metodo **`getUpdates`** serve a leggere quella coda: dentro ogni evento di messaggio c’è l’oggetto `chat` con l’`id` della conversazione. È questo numero che il bot deve usare come `chat_id` per inviarti i messaggi.
