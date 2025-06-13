```markdown
# iFunza

Welcome to iFunza, a comprehensive school management platform designed to streamline various administrative and academic processes. Our platform offers a suite of modules including Digital Diary, Bus Tracker, Invoice, Messages, Gradebooks, and Expense Management, all integrated to provide a seamless experience for schools, teachers, students, and parents.

## Features

- **Digital Diary**: Keep track of daily activities, assignments, and important notes.
- **Bus Tracker**: Monitor the real-time location of school buses for enhanced safety.
- **Invoice**: Manage and generate invoices efficiently.
- **Messages**: Communicate easily with students, parents, and staff.
- **Gradebooks**: Record and track student grades and academic performance.
- **Expense Management**: Handle school expenses with detailed tracking and reporting.

## Technology Stack

### Frontend

- **Next.js**: A powerful React framework for building server-side rendered applications.
- **GraphQL**: Query language for your API, providing a more efficient, powerful, and flexible alternative to REST.
- **React Query**: Data fetching library that simplifies the process of fetching, caching, synchronizing, and updating server state.
- **Zustand**: A small, fast, and scalable state management solution using simplified flux principles.
- **TypeScript**: A strict syntactical superset of JavaScript that adds optional static typing to the language.

### Backend

- **Fastify**: A fast and low overhead web framework for Node.js.
- **GraphQL**: API query language used for interacting with the database.
- **Prisma**: Next-generation ORM for Node.js and TypeScript.
- **Postgres**: Powerful, open-source object-relational database system.
- **MongoDB**: NoSQL database for modern, scalable applications.
- **Mercurius GraphQL**: GraphQL adapter for Fastify.
- **Queues**: Implementing background jobs and tasks processing.

### Mobile

- **Flutter**: A UI toolkit for building natively compiled applications for mobile, web, and desktop from a single codebase.

#### Other Tools
 - Mailgun
 - Africa’s Talking
 - Twilio
 - Google Firebase
 - AWS S3
 - Vercel (education credentials)
 - Pinata (education credentials)
 - Canva (content creation)

```plainText

┌───────────────────────────────────────────────────────────────────────────────────────────────────────┐
│                                                                                                       │
│                                           **Frontend Clients**                                         │
│                                                                                                       │
└───────────────────────────────────────────────────────────────────────────────────────────────────────┘
                               ▲                                      ▲
                               │                                      │
                               │                                      │
┌───────────────────────┐      │      ┌───────────────────────┐      │      ┌───────────────────────┐
│                       │      │      │                       │      │      │                       │
│   **Web App**         │      │      │    **Mobile App**     │      │      │    **Admin Dashboard** │
│   (Next.js + TS)      │──────┘      │    (Flutter)          │──────┘      │    (Next.js + TS)      │
│                       │             │                       │             │                       │
│  - Docker Container   │             │  - GraphQL Client     │             │  - Docker Container   │
│  - GraphQL Client     │             │  - Sentry Integration │             │  - GraphQL Client     │
│  - Sentry Integration │             │                       │             │  - Sentry Integration │
│                       │             └───────────────────────┘             │                       │
└───────────────────────┘                                                  └───────────────────────┘
                               ▲                                      ▲
                               │                                      │
                               │                                      │
┌───────────────────────────────────────────────────────────────────────────────────────────────────────┐
│                                                                                                       │
│                                          **GraphQL Gateway**                                          │
│                                                                                                       │
│  - Apollo Router / Apollo Federation                                                                  │
│  - Aggregates subgraphs (Legacy, E-Store, Wallet)                                                     │
│  - Handles Auth, Rate Limiting                                                                        │
│                                                                                                       │
└───────────────────────────────┬───────────────────────────────┬───────────────────────────────────────┘
                                │                               │
                                │                               │
                                ▼                               ▼
┌─────────────────────┐      ┌─────────────────────┐      ┌─────────────────────┐
│                     │      │                     │      │                     │
│    **Legacy**       │      │     **E-Store**     │      │     **Wallet**      │
│   (Microservice)    │      │   (Microservice)    │      │   (Microservice)    │
│                     │      │                     │      │                     │
│  - Docker Container │      │  - Docker Container │      │  - Docker Container │
│  - GraphQL Subgraph │      │  - GraphQL Subgraph │      │  - GraphQL Subgraph │
│  - RabbitMQ Client  │      │  - RabbitMQ Client  │      │  - RabbitMQ Client  │
│                     │      │                     │      │                     │
└──────────┬──────────┘      └──────────┬──────────┘      └──────────┬──────────┘
           │                            │                            │
           │                            │                            │
           ▼                            ▼                            ▼
┌─────────────────────┐      ┌─────────────────────┐      ┌─────────────────────┐
│                     │      │                     │      │                     │
│   **Postgres**      │      │   **Postgres**      │      │   **Postgres**      │
│  (Legacy DB)        │      │  (E-Store DB)       │      │  (Wallet DB)        │
│                     │      │                     │      │                     │
└─────────────────────┘      └─────────────────────┘      └─────────────────────┘
           ▲                            ▲                            ▲
           │                            │                            │
           └──────────────┬─────────────┘                            │
                          │                                          │
                          ▼                                          ▼
┌───────────────────────────────────────────────────────────────────────────────────────────────────────┐
│                                                                                                       │
│                                  **RabbitMQ (Message Broker)**                                        │
│                                                                                                       │
│  - Async events (e.g., "order_created", "payment_processed")                                          │
│                                                                                                       │
└───────────────────────────────────────────────────────────────────────────────────────────────────────┘
                                      ▲
                                      │
                                      ▼
┌─────────────────────┐      ┌─────────────────────┐      ┌─────────────────────┐
│                     │      │                     │      │                     │
│    **Sentry**       │      │   **Uptime Kuma**   │      │    **CI/CD**        │
│  (Error Tracking)   │      │  (Uptime Monitoring)│      │  (GitHub Actions)   │
│                     │      │                     │      │                     │
└─────────────────────┘      └─────────────────────┘      └─────────────────────┘
```


1. **Each Microservice Has Its Own Postgres DB**  
   - No shared database → better isolation.  
   - Example:  
     - `Legacy` → `Legacy DB`  
     - `E-Store` → `E-Store DB`  
     - `Wallet` → `Wallet DB`  

2. **RabbitMQ Still Connects All Services**  
   - Used for cross-service events (e.g., `E-Store` emits an event → `Wallet` consumes it).  

3. **Observability**  
   - **Sentry**: Logs errors from all services.  
   - **Uptime Kuma**: Tracks health of each service + dependencies (DBs, RabbitMQ).  


![GraphQL Gateway Flow](https://raw.githubusercontent.com/ifunza-com/.github/main/profile/mermaidchart.png)




## Contributing

We welcome contributions to improve iFunza. Please follow these steps to contribute:

1. Clone the repository.
2. Create a new branch (`git checkout -b feature-branch`).
3. Commit your changes (`git commit -am 'Add new feature'`).
4. Push to the branch (`git push origin feature-branch`).
5. Create a new Pull Request.


# RabbitMQ Installation & Configuration Guide for iFunza

## Table of Contents
1. [RabbitMQ Installation](#rabbitmq-installation)
2. [Delayed Message Plugin Setup](#delayed-message-plugin-setup)
3. [Post-Installation Configuration](#post-installation-configuration)
4. [Verification](#verification)

---

## RabbitMQ Installation

### Ubuntu/Debian Installation

1. Create an installation script:

```bash
#!/bin/sh

sudo apt-get install curl gnupg apt-transport-https -y

## Team RabbitMQ's main signing key
curl -1sLf "https://keys.openpgp.org/vks/v1/by-fingerprint/0A9AF2115F4687BD29803A206B73A36E6026DFCA" | sudo gpg --dearmor | sudo tee /usr/share/keyrings/com.rabbitmq.team.gpg > /dev/null
## Community mirror of Cloudsmith: modern Erlang repository
curl -1sLf https://github.com/rabbitmq/signing-keys/releases/download/3.0/cloudsmith.rabbitmq-erlang.E495BB49CC4BBE5B.key | sudo gpg --dearmor | sudo tee /usr/share/keyrings/rabbitmq.E495BB49CC4BBE5B.gpg > /dev/null
## Community mirror of Cloudsmith: RabbitMQ repository
curl -1sLf https://github.com/rabbitmq/signing-keys/releases/download/3.0/cloudsmith.rabbitmq-server.9F4587F226208342.key | sudo gpg --dearmor | sudo tee /usr/share/keyrings/rabbitmq.9F4587F226208342.gpg > /dev/null

## Add apt repositories maintained by Team RabbitMQ
sudo tee /etc/apt/sources.list.d/rabbitmq.list <<EOF
## Provides modern Erlang/OTP releases
##
deb [arch=amd64 signed-by=/usr/share/keyrings/rabbitmq.E495BB49CC4BBE5B.gpg] https://ppa1.rabbitmq.com/rabbitmq/rabbitmq-erlang/deb/ubuntu noble main
deb-src [signed-by=/usr/share/keyrings/rabbitmq.E495BB49CC4BBE5B.gpg] https://ppa1.rabbitmq.com/rabbitmq/rabbitmq-erlang/deb/ubuntu noble main

# another mirror for redundancy
deb [arch=amd64 signed-by=/usr/share/keyrings/rabbitmq.E495BB49CC4BBE5B.gpg] https://ppa2.rabbitmq.com/rabbitmq/rabbitmq-erlang/deb/ubuntu noble main
deb-src [signed-by=/usr/share/keyrings/rabbitmq.E495BB49CC4BBE5B.gpg] https://ppa2.rabbitmq.com/rabbitmq/rabbitmq-erlang/deb/ubuntu noble main

## Provides RabbitMQ
##
deb [arch=amd64 signed-by=/usr/share/keyrings/rabbitmq.9F4587F226208342.gpg] https://ppa1.rabbitmq.com/rabbitmq/rabbitmq-server/deb/ubuntu noble main
deb-src [signed-by=/usr/share/keyrings/rabbitmq.9F4587F226208342.gpg] https://ppa1.rabbitmq.com/rabbitmq/rabbitmq-server/deb/ubuntu noble main

# another mirror for redundancy
deb [arch=amd64 signed-by=/usr/share/keyrings/rabbitmq.9F4587F226208342.gpg] https://ppa2.rabbitmq.com/rabbitmq/rabbitmq-server/deb/ubuntu noble main
deb-src [signed-by=/usr/share/keyrings/rabbitmq.9F4587F226208342.gpg] https://ppa2.rabbitmq.com/rabbitmq/rabbitmq-server/deb/ubuntu noble main
EOF

## Update package indices
sudo apt-get update -y

## Install Erlang packages
sudo apt-get install -y erlang-base \
                        erlang-asn1 erlang-crypto erlang-eldap erlang-ftp erlang-inets \
                        erlang-mnesia erlang-os-mon erlang-parsetools erlang-public-key \
                        erlang-runtime-tools erlang-snmp erlang-ssl \
                        erlang-syntax-tools erlang-tftp erlang-tools erlang-xmerl

## Install rabbitmq-server and its dependencies
sudo apt-get install rabbitmq-server -y --fix-missing
```

2. Make the script executable and run it:

```bash
chmod +x install.sh
sudo ./install.sh
```

---

## Delayed Message Plugin Setup

### Plugin Installation

1. Download the latest delayed message plugin:

```bash
# Determine RabbitMQ version
RABBITMQ_VERSION=$(sudo rabbitmqctl status | sed -n 's/.*RabbitMQ version: \([0-9.]*\).*/\1/p')


# Download compatible plugin version
wget https://github.com/rabbitmq/rabbitmq-delayed-message-exchange/releases/download/v${RABBITMQ_VERSION}/rabbitmq_delayed_message_exchange-${RABBITMQ_VERSION}.ez -P /tmp
```

2. Install the plugin:

```bash
# Copy plugin to plugins directory
sudo cp /tmp/rabbitmq_delayed_message_exchange-${RABBITMQ_VERSION}.ez $(rabbitmqctl eval 'io:format("~s~n", [code:lib_dir("rabbitmq_server")])')/plugins/

# Enable plugin and restart
sudo systemctl restart rabbitmq-server
sudo rabbitmq-plugins enable rabbitmq_delayed_message_exchange

```

---

## Post-Installation Configuration

### Management UI & User Setup

1. Enable management plugin:

```bash
sudo rabbitmq-plugins enable rabbitmq_management
```

2. Create admin user (replace with secure credentials):

```bash
sudo rabbitmqctl add_user ifunza_admin YourSecurePassword123
sudo rabbitmqctl set_user_tags ifunza_admin administrator
sudo rabbitmqctl set_permissions -p / ifunza_admin ".*" ".*" ".*"
```

3. Disable default guest user (recommended for production):

```bash
sudo rabbitmqctl delete_user guest
```

---

## Verification

### Service Status Check

```bash
sudo systemctl status rabbitmq-server
```

### Plugin Verification

```bash
sudo rabbitmq-plugins list | grep delayed
```
Expected output:
```
[E*] rabbitmq_delayed_message_exchange
```

### Management UI Access

Access the management console at:
```
http://<your-server-ip>:15672
```
Access on the code at:
```
"amqp://myuser:mypassword@48.217.51.197";
```

### Connection Test

Test using the management UI or with the RabbitMQ CLI:

```bash
sudo rabbitmqctl ping
```

---

## Maintenance

### Logs Location
- Main log: `/var/log/rabbitmq/rabbit@$(hostname).log`
- Startup log: `/var/log/rabbitmq/rabbit@$(hostname)_startup.log`

### Common Commands
```bash
# Restart service
sudo systemctl restart rabbitmq-server

# Check queue status
sudo rabbitmqctl list_queues

# Check connections
sudo rabbitmqctl list_connections
```

For production environments, consider configuring:
- TLS for secure connections
- Cluster setup for high availability
- Proper monitoring and alerting

Document version: 1.0  
Last updated: ${current_date}

## License

iFunza is licensed under the MIT License. See the [LICENSE](LICENSE) file for more details.
```
