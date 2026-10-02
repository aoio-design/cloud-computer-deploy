# Cloud Computer

One container that gives you a Linux desktop with an AI agent living in it — plus the
film studio web app your agent works in.

This repository exists for one reason: so the machine can be deployed from a URL,
in a web panel, without typing commands.

## What you need

- A VPS with **Docker** installed (2 vCPU / 8 GB RAM is the minimum; 4 vCPU / 16 GB
  is recommended, because the desktop is streamed to your browser while your agent works)
- Access to your hosting panel's **Docker Manager**

## Before you deploy: change one line

Open `docker-compose.yml` and replace this:

```yaml
- PASSWORD=CHANGE-ME-BEFORE-DEPLOY
```

with your own password. That password unlocks your desktop, so treat it like a
house key and keep it in your password manager.

Optional: `CUSTOM_USER=studio` is the name you sign in with. Leave it as `studio`, or
change it to something you prefer.

## Deploy it

1. In your hosting panel, open **VPS → Manage → Docker Manager**.
2. Click **Compose → Compose from URL**.
3. Give the project a name (for example `cloud-computer`) and paste the address of this
   file — the raw link shown at the top of this repository's file view.
4. Click **Deploy**.

Docker downloads the image and starts the machine. Docker Manager shows the project as
**Running** when it is up.

## What happens on the first start

Nothing needs your attention. In order: the desktop comes up, the film studio starts, and
the agent installs itself. The agent install takes about **10 minutes** and runs in the
background.

## How you reach it

No ports are published on your server's public address — deliberately. You reach the
desktop through the secure address you set up yourself (your own tunnel and access gate),
which the setup guide walks through.

## Updating it later

- To apply a change you made to this file: **Docker Manager → your project → Update**.
- To pick up a newer machine image: press **Update** again after the image is published,
  or **Delete** the project and deploy it again. Your data is untouched either way,
  because it lives in the folders below.

## Where your data lives

Three folders are created beside this file on your server:

| Folder | What is in it |
|---|---|
| `config` | Your desktop's settings and its home folder |
| `agent-home` | Your agent: its program, its memory, its skills, and your studio |
| `shared` | A folder both the desktop and the agent can use |

These are on your server, not inside the container, so updating or rebuilding the container
never removes your agent, your conversations or your studio.
