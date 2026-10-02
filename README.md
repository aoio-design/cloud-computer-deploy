# Cloud Computer

One container that gives you a Linux desktop with an AI agent living in it — plus the
film studio web app your agent works in.

This repository holds the machine's definition in one place, so the block you paste into
your hosting panel is always the current one. The same block is printed in your setup guide.

## What you need

- A VPS with **Docker** installed (2 vCPU / 8 GB RAM is the minimum; 4 vCPU / 16 GB
  is recommended, because the desktop is streamed to your browser while your agent works)
- Access to your hosting panel's **Docker Manager**

## Before you deploy: change one line

In `docker-compose.yml`, replace this:

```yaml
- PASSWORD=CHANGE-ME-BEFORE-DEPLOY
```

with your own password. That password unlocks your desktop, so treat it like a
house key and keep it in your password manager. There is no reset email for it.

Optional: `CUSTOM_USER=studio` is the name you sign in with. Leave it as `studio`, or
change it to something you prefer.

## Deploy it

1. In your hosting panel, open **VPS → Manage → Docker Manager**.
2. Click **Compose → Compose manually**.
3. Give the project the name `cloud-computer`.
4. Select everything already in the editor, then replace it with the whole of
   `docker-compose.yml` from this repository — with your password change in place.
5. Click **Deploy**.

Docker downloads the machine image and starts it. **A few minutes, and you do not need to
watch it.** Your project reports **Running** when the machine is up.

## What happens on the first start

Nothing needs your attention. In order: the desktop comes up, the film studio starts, and
the agent installs itself. The agent install takes about **10 minutes** and runs in the
background.

The machine also asks for your city the first time you sign in to the desktop, and remembers
it. That is why no time zone is set in this file — one set here would override your answer.

## How you reach it

No ports are published on your server's public address — deliberately. You reach the
desktop through the secure address you set up yourself (your own tunnel and access gate),
which the setup guide walks through.

## Updating it later

- To apply a change you made to this file: **Docker Manager → your project → Update**.
- To pick up a newer machine image: press **Update** again after a new image is published.
  Your data is untouched either way, because it lives in the folders below.

## Where your data lives

Three folders are created beside this file on your server:

| Folder | What is in it |
|---|---|
| `config` | Your desktop's settings and its home folder |
| `agent-home` | Your agent: its program, its memory, its skills, and your studio |
| `shared` | A folder both the desktop and the agent can use |

These are on your server, not inside the container, so updating or rebuilding the container
never removes your agent, your conversations or your studio.
