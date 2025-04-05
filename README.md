# SalesBot - WhatsApp Advertisement Automation

## Overview

SalesBot is a specialized HTTP server developed to automate the distribution of promotional content within WhatsApp groups, primarily designed to serve the marketing needs of small and medium-sized businesses. By streamlining and automating message management and scheduling, SalesBot significantly reduces manual effort, enhances customer engagement, and increases the consistency and effectiveness of digital marketing campaigns.

## Purpose and Practical Benefits

Small businesses often rely heavily on targeted messaging in local and niche WhatsApp groups to drive engagement and sales. However, manual management of these interactions can be time-consuming, prone to errors, and difficult to scale.

SalesBot addresses these challenges by:

- Providing centralized storage for advertisement messages.
- Allowing easy insertion, updating, and deletion of messages.
- Automating scheduled distribution according to custom-configured days and times.
- Offering intuitive tools for message prioritization and usage limitation.
- Simplifying WhatsApp account management through remote QR-code-based authentication.
- Eliminating repetitive tasks and significantly reducing the chance of human error.

By automating these tasks, SalesBot empowers small businesses to consistently reach their audience at optimal times with tailored marketing messages, thus improving business efficiency and effectiveness.

## Features and Capabilities

### Message Management
- **Insertion, updating, and deletion:** Simple and intuitive RESTful API to manage message lifecycle.
- **Message prioritization:** Control delivery order based on customizable priority levels.
- **Usage limits:** Set limits on the frequency of specific messages to maintain optimal relevance.

### Scheduling and Automation
- **Custom scheduling:** Messages are automatically sent at specified days and hours.
- **Automated dispatch:** Completely hands-off message delivery, ensuring timely outreach.

### WhatsApp Account Management
- **QR-based authentication:** Convenient remote session login and management via dynamically generated QR codes.
- **Profile management:** Easy reset or removal of WhatsApp sessions directly from the interface.

### Logging and Monitoring
- Detailed logs for real-time tracking and troubleshooting.

## Technologies Used

SalesBot leverages robust, reliable technologies that combine ease of use, security, and scalability:

- **Python:** Core server and client application logic.
- **Selenium WebDriver:** Automates interaction with WhatsApp Web for seamless message delivery.
- **ngrok:** Secure tunneling service providing external accessibility to the local server.
- **Gradio (hosted on Hugging Face):** A simple yet powerful web-based user interface offering remote server control, configuration management, and monitoring.
- **GitHub Gist Integration:** Dynamically updates the public server endpoint for uninterrupted client-server communication.

## Architecture

SalesBot consists of three main components:

- **HTTP Server:** Manages message storage, scheduling, sending logic, and RESTful interactions.
- **Python Client:** Provides an SDK-like interface for easy integration and remote operations.
- **Frontend Interface (Gradio):** Offers an intuitive, browser-based UI for non-technical users to control and monitor operations remotely.
