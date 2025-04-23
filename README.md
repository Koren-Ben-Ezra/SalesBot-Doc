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
  - **Text**
  - **URL** (optional)
  - **Priority** (higher goes first)
  - **Usage Limit** (how many times to send)
  - **Usage** (how many time the message was sent)

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

## 5. UI Screenshots


### Server control panel
![image](https://github.com/user-attachments/assets/05ab27ff-a499-4860-8a83-8bd617f190ce)

### Inserting a message
![image](https://github.com/user-attachments/assets/a2ce7654-a63b-4089-8422-92cf527da10a)

### Updating a message
![image](https://github.com/user-attachments/assets/ceb3bb66-0f48-40a4-9b5e-55b536b9c058)

### Peek next message
![image](https://github.com/user-attachments/assets/1858a520-70e8-4d5e-9016-4ddf675b3651)

### Server settings panel
![image](https://github.com/user-attachments/assets/1e5d9008-f41e-465e-9330-9cf6dc909c2d)
