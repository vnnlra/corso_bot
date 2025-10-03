# Bot Telegram minimale in Java (Java 8)

Questo esempio mostra come inviare messaggi a un **bot Telegram** usando solo le librerie standard di Java 8, senza librerie esterne.

---

## Classe `NoteBotMin.java`

```java
import java.net.*;
import java.io.*;

public class NoteBotMin {
    private final String token;
    private final String chatId;

    public NoteBotMin(String token, String chatId) {
        this.token = token;
        this.chatId = chatId;
    }

    public void sendMessage(String msg) throws Exception {
        String urlStr = "https://api.telegram.org/bot" + token + "/sendMessage"
                + "?chat_id=" + chatId
                + "&text=" + URLEncoder.encode(msg, "UTF-8");

        URL url = new URL(urlStr);
        HttpURLConnection conn = (HttpURLConnection) url.openConnection();

        // Imposta il metodo della richiesta HTTP.
        // In questo caso sarebbe superfluo (il default è già GET),
        // ma lo lasciamo qui come "anticipazione":
        // quando studieremo le comunicazioni REST vedremo meglio
        // cosa significa GET, POST, ecc.
        conn.setRequestMethod("GET");

        BufferedReader in = new BufferedReader(new InputStreamReader(conn.getInputStream()));
        String line;
        while ((line = in.readLine()) != null) {
            System.out.println(line);
        }
        in.close();
    }

    public static void main(String[] args) {
        String token = "IL_TUO_TOKEN";
        String chatId = "IL_TUO_CHAT_ID";

        NoteBotMin bot = new NoteBotMin(token, chatId);

        try {
            bot.sendMessage("Ciao dal bot Java!");
            bot.sendMessage("Promemoria: porta la chiavetta USB domani!");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

---

## Come funziona

1. Inserisci il tuo **token** (dato da [BotFather](https://core.telegram.org/bots#botfather)) e il tuo **chatId** (ottenuto con `getUpdates` dopo aver scritto un messaggio al bot).  
2. Compila ed esegui il programma.  
3. Ogni volta che chiami `bot.sendMessage("testo")` il bot ti invierà un messaggio su Telegram.  

---

👉 Questo è un esempio **essenziale**, pensato per introdurre l’uso di un bot senza entrare nei dettagli delle comunicazioni HTTP, che verranno approfondite in seguito quando si studieranno le API REST.
