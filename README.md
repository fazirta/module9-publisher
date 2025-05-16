## How much data your publisher program will send in one run?

In one run the publisher sends **5** events. Each event is serialized by Borsh as two strings—`user_id` and `user_name`. Borsh writes each string as a 4-byte little-endian length prefix followed by the UTF-8 bytes. For our values:

- `user_id = "1"` → 4 bytes (length) + 1 byte (content) = **5 bytes**  
- `user_name = "125900004y-Amir"` → 4 bytes (length) + 15 bytes (content) = **19 bytes**

Total per event: 5 + 19 = **24 bytes**  
Total for 5 events: 5 × 24 = **120 bytes** of payload data

---

## What does `amqp://guest:guest@localhost:5672` mean?

- **amqp**: use the AMQP protocol  
- **guest** (first): the username  
- **guest** (second): the password  
- **localhost:5672**: the RabbitMQ broker’s host and port  

---

## Sending and processing events

![Publisher and Subscriber Consoles](./img/89675224-9176-48d6-9fcb-2b3e576fda17.png)

1. In the **subscriber** directory I ran:
   ```bash
   cargo run
   ````

   The subscriber connected to RabbitMQ and waited for messages.

2. In the **publisher** directory I ran:

   ```bash
   cargo run
   ```

   The publisher sent 5 `UserCreatedEventMessage` events to the broker.

3. Immediately in the subscriber console I saw log lines for each of the 5 events, for example:

   ```
   In Fazil’s Computer [2306274983]. Message received: UserCreatedEventMessage { user_id: "1", user_name: "2306274983-Amir" }
   ...
   In Fazil’s Computer [2306274983]. Message received: UserCreatedEventMessage { user_id: "5", user_name: "2306274983-Emir" }
   ```

   This confirms that all 5 events were published by the publisher and successfully consumed by the subscriber.
