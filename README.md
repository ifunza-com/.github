
![GraphQL Gateway Flow](https://raw.githubusercontent.com/ifunza-com/.github/main/profile/mermaidchart.png)

the code
---
config:
  layout: fixed
---
flowchart TD
    Web["Web App (Next.js)"] --> Gateway["GraphQL Gateway"] & Sentry["Sentry"]
    Mobile["Mobile App (Flutter)"] --> Gateway & Sentry
    Admin["Admin Dashboard (Next.js)"] --> Gateway & Sentry
    Gateway --> Legacy["Legacy Service"] & EStore["E-Store Service"] & Wallet["Wallet Service"]
    Legacy --> LegacyDB[("Legacy Postgres")] & RabbitMQ[("RabbitMQ")] & Sentry
    EStore --> EStoreDB[("E-Store Postgres")] & RabbitMQ & Sentry
    Wallet --> WalletDB[("Wallet Postgres")] & RabbitMQ & Sentry
    Uptime["Uptime Kuma"] -.-> Web & Mobile & Legacy & EStore & RabbitMQ
    CI["CI/CD"] -.-> Web & Admin & Legacy & EStore & Wallet
