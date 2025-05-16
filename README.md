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
