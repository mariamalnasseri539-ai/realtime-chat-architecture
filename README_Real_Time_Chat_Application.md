# 💬 Real-Time Chat Application

A **Real-Time Chat Application** based on a **Client–Server architecture**, allowing users to sign in with their email and communicate through instant text and voice messages. The system tracks message status (Sent ✓ / Delivered ✓ / Read ✓✓), preserves conversation history, and supports message deletion and push notifications for new messages.

This repository contains the full software engineering design of the system: use cases, class diagram, sequence diagrams, state diagram, software architecture, deployment diagram, and design patterns.

---

## 🎯 Design Goals

- **Real-Time Support** — bidirectional communication via WebSocket for instant message delivery
- **Security** — identity verification through an authentication service, with passwords stored securely using hashing
- **Scalability** — layered design (Presentation, Application, Data) to enable load distribution across servers
- **Reliability** — guaranteed message delivery even after a temporary disconnection (resend on reconnect)
- **Maintainability** — clear separation between UI, business logic, and database so each part can evolve independently

---

## 🏗️ System Architecture

### Client Side
- **User UI:**
  - Registration via Gmail
  - Sending/receiving text and audio messages
  - Message status display (Sent ✓, Delivered ✓, Read ✓✓)
  - Viewing chat history
  - Deleting text or audio messages

### Web Server
- **Chat Application Core** — main component handling requests from the client UI
- **Business Logic** — handles registration, sending messages, viewing history, deleting messages
- **Authentication** — verifies user identity via Gmail
- **Messaging Service** — manages message delivery and tracks message state (Sent/Delivered/Read)
- **Notification Service** — pushes notifications for new incoming messages

### API Layer
- **WebSocket API** — real-time, two-way communication for instant delivery
- **RESTful API** — endpoints for non-real-time operations (registration, chat history, deletion)

### Database Server
- **DBMS** — stores user data, messages (with status), and chat history
- **Data stored:** Users, Messages, Chats

---

## 🔌 Interface Specification

### RESTful API
| Endpoint | Method | Description |
|---|---|---|
| `/api/register` | `POST` | `{email, password}` → create a new account |
| `/api/chats/{id}/history` | `GET` | Retrieve conversation history |
| `/api/messages/{id}` | `DELETE` | Delete a specific message |

### WebSocket API
| Action / Event | Description |
|---|---|
| `joinChat(chatId)` | Join a conversation to receive messages |
| `sendMessage(chatId, content, type)` | Send a message (text/voice) |
| `messageCreated(message)` | Event: a new message was received |
| `messageUpdated(status)` | Event: message status updated (Delivered/Read) |

---

## 🗄️ Data Management

The system uses a **Relational Database**:

| Table | Description |
|---|---|
| **Users** | User data (ID, email, password, status, last seen) |
| **Contacts** | Contact lists with blocking and nickname features |
| **Chats** | One-to-one and group conversations |
| **Conversation Participants** | Members of each conversation and their roles (Member / Moderator / Owner) |
| **Messages** | Text and voice messages with metadata (sender, content, duration, size) |
| **Message Recipients** | Per-recipient message status (Sent, Delivered, Read) with timestamps |

Data integrity is enforced through constraints (`PK`, `FK`, `UNIQUE`), and performance is optimized with indexes for faster search and retrieval.

---

## 🖥️ Hardware–Software Mapping

**Hardware:**
- **Server:**
  - Web Server — handles requests
  - Database Server — stores and manages data
- **Client Devices:** computers or smartphones running the chat app
- **Network:** stable internet connection supporting HTTP/HTTPS and WebSocket

**Software:**
- **Client Application** — web/mobile app for user interaction
- **Application Server** — hosts business logic, messaging, and notification services
- **Database** — relational DBMS (e.g., MySQL or PostgreSQL)
- **Communication Protocols:**
  - RESTful API for non-real-time operations
  - WebSocket for real-time communication

---

## 📐 UML Diagrams & Design Artifacts

This repository includes the full set of design diagrams (Edraw `.eddx` format) covering the system's software engineering design:

| File | Diagram |
|---|---|
| `Use_Cuse_Digram.eddx` / `Use_Cuse_Digram2.eddx` | Use Case Diagrams |
| `use_case_des.eddx` | Use Case Description |
| `class_diagram.eddx` | Class Diagram |
| `Text_Message_Sending_Sequnce_Diagram_.eddx` | Sequence Diagram — Sending a Text Message |
| `Audio_Message_Sending_Sequnce_Diagram_.eddx` | Sequence Diagram — Sending an Audio Message |
| `View_Message_Sequnce_Diagram_.eddx` | Sequence Diagram — Viewing Messages |
| `State_Diagram_Of_Message2.eddx` | State Diagram — Message Lifecycle |
| `Interface_Specifiation_Diagram_.eddx` | Interface Specification Diagram |
| `layer_.eddx` | Layered Architecture Diagram |
| `deployment.eddx` | Deployment Diagram |
| `facade.eddx` | Facade Design Pattern Diagram |
| `non__functional.eddx` | Non-Functional Requirements Diagram |
| `Architecture_.docx` | Client–Server Architecture Document |
| `Real_time_chat_Application.docx` | Full Project Design Document |

> 📝 `.eddx` files can be opened with [Edraw Max](https://www.edrawsoft.com/edraw-max/) (or WPS/compatible diagramming tools that support the format).

---

## 📁 Suggested Repository Structure

```
Real-Time-Chat-Application/
├── docs/
│   ├── Architecture_.docx
│   ├── Real_time_chat_Application.docx
│   ├── Use_Cuse_Digram.eddx
│   ├── Use_Cuse_Digram2.eddx
│   ├── use_case_des.eddx
│   ├── class_diagram.eddx
│   ├── Text_Message_Sending_Sequnce_Diagram_.eddx
│   ├── Audio_Message_Sending_Sequnce_Diagram_.eddx
│   ├── View_Message_Sequnce_Diagram_.eddx
│   ├── State_Diagram_Of_Message2.eddx
│   ├── Interface_Specifiation_Diagram_.eddx
│   ├── layer_.eddx
│   ├── deployment.eddx
│   ├── facade.eddx
│   └── non__functional.eddx
└── README.md
```

---

## 🚧 Project Status

This repository currently contains the **software engineering design phase** of the project (use cases, architecture, class/sequence/state diagrams, interface specification, and deployment plan). Implementation of the client, server, and database layers follows this design.

---

## 📄 License

This project is an academic/educational software engineering design project.
