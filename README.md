# RabbitMQ Testing & Exploration 🐰📬

Welcome to my RabbitMQ testing playground!  
This repository contains simple, focused experiments to help me understand how to work with RabbitMQ in .NET applications.

---

## 🎯 Purpose

I'm exploring RabbitMQ messaging patterns, features, and integration with C# to:

- Understand core concepts like **exchanges**, **queues**, and **routing**
- Test various **exchange types**: direct, fanout, topic, headers
- Practice with **.NET clients** (console apps using [RabbitMQ.Client](https://www.nuget.org/packages/RabbitMQ.Client))
- Prepare for integrating RabbitMQ into real-world projects

---

## 🛠️ Tech Stack

- **Language**: C#
- **Platform**: .NET 6/7 Console Applications
- **Message Broker**: RabbitMQ (local instance via Docker or installed manually)
- **Client Library**: [RabbitMQ.Client](https://github.com/rabbitmq/rabbitmq-dotnet-client)

---

## 🚀 Getting Started

### Prerequisites

- [.NET SDK](https://dotnet.microsoft.com/download)
- RabbitMQ instance (locally or via Docker)

<details>
<summary>💡 Run RabbitMQ via Docker</summary>

~~~~bash
docker run -d --hostname rabbit-host --name rabbitmq-dev \
  -p 5672:5672 -p 15672:15672 \
  rabbitmq:3-management
~~~~

Access management UI: [http://localhost:15672](http://localhost:15672)  
(Default user/pass: `guest` / `guest`)
</details>

---

### ⚙️ Configuration

Before running the project, update the RabbitMQ connection settings in your code (typically in the `Sender` and `Receiver` projects):

~~~~csharp
var factory = new ConnectionFactory()
{
    HostName = "192.168.106.121",
    UserName = "user1",
    Password = "user1"
};
~~~~

#### 🔐 Replace these with your own RabbitMQ settings:

| Setting    | Description                                       |
|------------|---------------------------------------------------|
| `HostName` | The IP address or hostname of your RabbitMQ server |
| `UserName` | Your RabbitMQ username                            |
| `Password` | Your RabbitMQ password                            |

#### 💡 Example (for local setup with default guest user):

~~~~csharp
HostName = "localhost",
UserName = "guest",
Password = "guest"
~~~~

Make sure your RabbitMQ server is reachable from your environment and that the necessary ports (`5672` for AMQP and `15672` for the management UI) are open.

---

### ▶️ Run the Sample

~~~~bash
dotnet restore
dotnet build
dotnet run --project Sender
dotnet run --project Receiver
~~~~

---

## 🧪 Experiments in This Repo

| Folder / Project   | Description                           |
|--------------------|---------------------------------------|
| `BasicSendReceive` | Simple producer/consumer              |
| `WorkQueues`       | Simulates round-robin worker queues   |
| `Routing`          | Uses `direct` exchange to route logs  |
| `Topics`           | Wildcard-based routing via topic exchange |
| `RPCs`             | Remot Procedure Call based on RabbitMQ |

---

## 📚 References

- [RabbitMQ Tutorials for .NET](https://www.rabbitmq.com/tutorials/tutorial-one-dotnet.html)
- [RabbitMQ Documentation](https://www.rabbitmq.com/documentation.html)
- [RabbitMQ.Client on NuGet](https://www.nuget.org/packages/RabbitMQ.Client)

---

## 👨‍💻 Author

**Emad Ghosi**  
🔗 [emadg-dev.github.io](https://emadg-dev.github.io)

---

## 📄 License

This project is licensed under the **MIT License**, except for any files derived from the [rabbitmq/rabbitmq-tutorials](https://github.com/rabbitmq/rabbitmq-tutorials) repository, which are subject to the **Mozilla Public License 2.0 (MPL-2.0)**.

Please see the [`LICENSE`](./LICENSE) file for full details.
