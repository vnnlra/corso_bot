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

