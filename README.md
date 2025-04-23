# SalesBot Architecture Overview

## 1. High-Level View
At its core, SalesBot runs a **Flask** server on a Raspberry Pi that:
- Exposes a simple REST API for creating, updating and deleting messages  
- Manages scheduled jobs that decide *when* to send  
- Drives a Chrome via **Selenium** to actually *send* messages through WhatsApp Web to a dedicated group  

A thin **Python client library** wraps those HTTP calls into easy methods, and a **Gradio UI** sits on top. The UI simply calls the client, which in turn calls the server.

---

## 2. Dynamic ngrok in a Nutshell
Instead of a fixed IP, SalesBot launches an **ngrok** tunnel at startup and writes its public URL to a GitHub Gist. Clients read that Gist to find the current address, so the server can reboot (and get a fresh ngrok link) without any manual URL updates.

---

## 3. Core Data Structures
- **Message**  
  - **ID** (UUID)  
  - **Text** + optional **URL**  
  - **Priority** (higher goes first) and **Usage Limit** (how many times to send)  

- **MessageStore**  
  - A priority queue (min-heap) that always serves the highest-priority, lowest-usage message next  
  - Persists to `messages.json` so your queue survives restarts
  - Backups for the message store are done in a lazy approach

- **Scheduler**  
  - Uses APScheduler to turn each queued message into a “send” job  
  - Calculates daily time slots (with configurable hours + random jitter) and enqueues them  

---

## 4. Three Standout Features
1. **Instant “Send Now”**  
   One API call (and one button in the UI) pulls the next message from the queue and fires it off immediately—perfect for urgent alerts.

2. **QR-Based Login Persistence**  
   On first run, Selenium grabs the WhatsApp Web QR code as an image and send it to the client (displayed on the UI). The client scan it once, and the server’s Chrome profile stays logged in indefinitely.

3. **Automated, Jittered Scheduling**  
   Define active days and time windows; the Scheduler spaces out the queue automatically, adding a bit of randomness so messages don’t look robotic.
