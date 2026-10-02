# Cloud Computer

One container that gives you a Linux desktop with an AI agent living in it — plus the
film studio web app your agent works in.

This repository holds the machine's definition in one place, so the file your hosting panel
points at is always the current one. The same setup is described in your guide.

## What you need

- A VPS with **Docker** installed (2 vCPU / 8 GB RAM is the minimum; 4 vCPU / 16 GB
  is recommended, because the desktop is streamed to your browser while your agent works)
- Access to your hosting panel's **Docker Manager**

## Deploy it

1. In your hosting panel, open **VPS → Manage → Docker Manager**.
2. Click **Compose → Compose from URL**.
3. Give the project the name `cloud-computer`, and paste this address into the URL field:

   ```
   https://raw.githubusercontent.com/aoio-design/cloud-computer-deploy/main/docker-compose.yml
   ```

4. Click **Deploy**.

Docker downloads the machine image and starts it. **A few minutes, and you do not need to
watch it.** Your project reports **Running** when the machine is up.

## Then set your desktop password

This file ships with a placeholder password, because a file anyone can download cannot carry
yours. Replace it before your machine gets an address:

1. Open your project in Docker Manager and open its **YAML editor**.
2. Find the line `- PASSWORD=CHANGE-ME-BEFORE-DEPLOY` and put your own password there.
3. Optional: the line above it, `- CUSTOM_USER=studio`, is the name you sign in with.
4. Save it and let Docker apply the change.

Treat that password like a house key and keep it in your password manager — it unlocks your
desktop, and there is no reset email for it.

Until your machine is given a public address, the placeholder cannot be reached from
anywhere, so there is no hurry — but there is also no reason to wait.

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

- To apply a change: **Docker Manager → your project → Update**.
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
