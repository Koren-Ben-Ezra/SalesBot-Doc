# SalesBot - WhatsApp Advertisement Automation

Note: The source code is not publicly available due to business confidentiality.

## Overview

SalesBot is a specialized HTTP server developed to automate the distribution of promotional content within WhatsApp groups, primarily designed to serve the marketing needs of small and medium-sized businesses. By streamlining and automating message management and scheduling, SalesBot significantly reduces manual effort, enhances customer engagement, and increases the consistency and effectiveness of digital marketing campaigns.

## Purpose and Practical Benefits

Small businesses often rely heavily on targeted messaging in local and niche WhatsApp groups to drive engagement and sales. However, manual management of these interactions can be time-consuming, prone to errors, and difficult to scale.

With SalesBot all you have to do is:

0. Config the server settings for your needs
1. Insert a stack of messages with a priority & usage limit
2. Thats it.

## Architecture

- **HTTP Server** – Responsible for:
  - Maintaining the message store
  - Automating sending of the next message
  - Managing message scheduling and configuration
  - Handling WhatsApp authentication and session control

- **Client API** – Responsible for:
  - Providing a simplified Python interface for developers
  - Communicating with the HTTP server over HTTP(S)
  - Automatically fetching the current ngrok URL from a GitHub Gist

- **Client App (Gradio Frontend + Hugging Face Space)** – Responsible for:
  - Providing a user-friendly web interface for message and server management
  - Allowing non-technical users to view, insert, update, and delete messages
  - Supporting WhatsApp session login via QR code

## Technologies Used
- **Python:** Core server and client application logic.
- **Selenium WebDriver:** Automates interaction with WhatsApp Web for seamless message delivery.
- **ngrok:** Secure tunneling service providing external accessibility to the local server.
- **Gradio (hosted on Hugging Face):** A user interface offering remote server control, configuration management, and monitoring.
- **GitHub Gist Integration:** Dynamically updates the public server endpoint for uninterrupted client-server communication.


## App Screenshots
![image](https://github.com/user-attachments/assets/197a9444-c89e-4439-b469-643eacfd8ebc)


![image](https://github.com/user-attachments/assets/5467d56b-9dbc-416c-8f09-8cdcaf2c0062)
