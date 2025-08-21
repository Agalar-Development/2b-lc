# 2b-lc
 2b2t live chat and tab built with fabric, can be used with headless-mc

[Support Server](https://discord.gg/5trvjuqgm8)

# How to use
- It starts a TCP server on the headless-mc, to get chat and tab list just connect localhost:9090 
- Giving the chat logs as it is and since 2b2t chat uses <> indicators for playernames a chat message should look like:

```<Luxotick>: How to use this?```

- I seperated the tablist from the chat messages with adding indicator for it so the tablist messages, an example of it:

```Tab list: Luxotick CrawLeyYou```

- You can seperate usernames with checking the blanks in the message from the server

- It also gets the death messages too it has no indicators so you can seperate it by using the "no indicator" example:

```Luxotick broke their neck, and the rest of their body.```

Example usage with java:
```java
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.net.Socket;

public class TCPChatClient {
    public static void main(String[] args) {
        String serverAddress = "localhost"; // Change if needed
        int port = 9090;

        try (Socket socket = new Socket(serverAddress, port);
             BufferedReader in = new BufferedReader(new InputStreamReader(socket.getInputStream()))) {

            System.out.println("Connected to 2b-lc server at " + serverAddress + ":" + port);

            String message;
            while ((message = in.readLine()) != null) {
                processMessage(message);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    private static void processMessage(String message) {
        if (message.startsWith("Tab List: ")) {
            // Tab list update
            String tabList = message.substring(10); // Remove "Tab List: "
            System.out.println("[TAB LIST] " + tabList);
        } else if (message.startsWith("<") && message.contains(">: ")) {
            // Player chat message
            System.out.println("[CHAT] " + message);
        } else {
            // Death message (no special indicator)
            System.out.println("[DEATH] " + message);
        }
    }
}
```

I hate workflows
