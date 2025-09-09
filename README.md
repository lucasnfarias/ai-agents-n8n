# ai-agents-n8n

```mermaid
---
config:
  theme: redux
  layout: dagre
---
flowchart LR
    A(["WhatsApp"]) --> B{"Webhook (n8n)"}
    B --> D["UserInfo (supabase)"]
    D --> n1(["HiL (block)"])
    n1 --> n3["ParseMessage"]
    n3 --> n4["MessageQueue"]
    n4 --> n5["IA"]
    n5 --> n2(["HiL (block)"])
    n2 --> n6["Response"]
    n6 -.-> A
    n7["ErrorCatch"] --> n8["Webhook Discord"]
    n3@{ shape: hex}
    n4@{ shape: hex}
    n5@{ shape: trap-b}
    n6@{ shape: trap-t}
    n7@{ shape: rounded}
    n8@{ shape: diam}

```

WhatsApp AI Agent made with n8n

- Create a environment on VPS with Docker + [Coolify](https://coolify.io/)
- Deploy a [N8N](https://n8n.io/) distributed structure (Editor, Worker, Webhook)
- Configure [Supabase](https://supabase.com/), [Redis](https://redis.io/) and [PostgreSQL](https://www.postgresql.org/)
- Integrate with [Evolution API](https://doc.evolution-api.com/v1/pt/get-started/introduction) that will be the bridge to WhatsApp

## Installation

1. We used Hetzner to host our Coolify and other tools
2. Created a domain on HostGator (test-app-lucas.shop) and setup rule/register `A | *.test-app-lucas.shop.` to point to Hetzner server IP
3. We installed Coolify on Hetzner server by running this command via ssh: `curl -fsSL https://cdn.coollabs.io/coolify/install.sh | sudo bash`
4. Updated Coolify setting to point to https://coolify.test-app-lucas.shop
5. Created a project and add Supabase as a project resource on Coolify
6. Updated supabase domain to https://supabase.test-app-lucas.shop and deployed it
7. Created the `docker-compose.yml` to configure all the necessary containers for our infra WhatsApp N8N Agent
8. Update N8N and Evolution API domains

## Containers

- [N8N (main, worker and webhook)](https://docs.n8n.io/hosting/configuration/environment-variables/)
- Postgres
- Redis
- [Evolution API](https://doc.evolution-api.com/v1/pt/env)

## N8N
- We use the [Queue Mode](https://docs.n8n.io/hosting/scaling/queue-mode/)
<img width="752" height="261" alt="image" src="https://github.com/user-attachments/assets/c48397f7-0047-4ecc-ad8a-1f72033b1da1" />
