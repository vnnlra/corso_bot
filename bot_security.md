### Note su sicurezza, privacy e scelta del nome

Quando si crea un bot Telegram è importante fare attenzione ad alcuni aspetti di **sicurezza e privacy**. Il *token* fornito da [@BotFather](https://t.me/BotFather) è una **chiave segreta** che consente a chiunque la conosca di controllare il bot: **non deve mai essere condiviso** né pubblicato su Internet (ad esempio in repository GitHub o forum). Se il token viene esposto, va immediatamente rigenerato tramite BotFather. Inoltre, il bot non deve mai memorizzare o trasmettere informazioni personali degli utenti senza il loro consenso, e le conversazioni dovrebbero essere progettate in modo da non raccogliere dati sensibili.

È anche importante sapere che **ogni bot ha un nome utente univoco**, che può essere usato per generare automaticamente link del tipo `https://t.me/<nomebot>`. Questo significa che altri bot o script potrebbero tentare di contattare il vostro bot generando casualmente indirizzi. Per evitare abusi, è consigliabile implementare **controlli sull’identità degli utenti** (ad esempio verificando l’`id` Telegram dell’utente autorizzato) e ignorare richieste provenienti da account sconosciuti.

In **PHP**, l’identificativo dell’utente si trova solitamente in:

```php
$id = $update['message']['from']['id'];
```

In **Java**, può essere ottenuto da:

```java
Long id = update.getMessage().getFrom().getId();
```

Confrontando questo valore con quello dell’utente autorizzato si può filtrare chi può interagire con il bot.

Per quanto riguarda il **nome**, scegli un nome riconoscibile ma rispettoso: evita riferimenti offensivi o ambigui, e preferisci nomi chiari che descrivano lo scopo del bot (ad esempio *WeatherHelperBot* o *QuizScuolaBot*). Il nome utente del bot deve terminare obbligatoriamente con **“Bot”**.
