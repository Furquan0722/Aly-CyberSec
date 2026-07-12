# 🛡️ Episode 01 – Host & Network Penetration Testing

> *"Every successful penetration test begins with understanding the target before attacking it."*

---

# 📘 Episode Overview

Welcome to the first episode of **Ali's CyberSec Handbook**.

This episode documents the complete attack methodology used during one of the first practical penetration testing scenarios encountered in the eJPT learning journey.

Instead of treating every topic as an isolated concept, this episode follows the mindset of a professional penetration tester. Every tool, command, and technique is introduced exactly when it becomes necessary during the attack.

By the end of this episode, you will understand not only **how** each tool works, but also **why** it is used and **when** it should be used during a real penetration test.

---

# 🌍 Real World Scenario

Imagine you have been hired by a company to perform an internal penetration test.

During reconnaissance, you discover a Microsoft IIS web server with **WebDAV** enabled.

At first glance, it appears to be a normal file-sharing service.

However...

A professional penetration tester never assumes a service is secure.

Instead, they begin asking questions:

- Can I upload files?
- Which file extensions are allowed?
- Can uploaded files be executed?
- Can I generate a payload?
- Can I gain remote access?
- What happens after I obtain a shell?

Every chapter in this episode answers one of these questions.

By the end of the attack chain, a simple WebDAV service becomes the entry point to complete system access.

---

# 🎯 Learning Objectives

After completing this episode, you should be able to:

- Understand how WebDAV works.
- Identify insecure WebDAV configurations.
- Test upload permissions using **davtest**.
- Generate payloads using **msfvenom**.
- Upload payloads using **Cadaver**.
- Configure a Metasploit Handler.
- Understand Reverse TCP payloads.
- Obtain a Meterpreter session.
- Understand the relationship between PostgreSQL and Metasploit.
- Follow a complete attack chain from reconnaissance to post-exploitation.

---

# 📚 Topics Covered

| Chapter | Topic | Status |
|----------|-------|--------|
| 01 | WebDAV | ✅ |
| 02 | davtest | ✅ |
| 03 | msfvenom | ✅ |
| 04 | Reverse Shell | ✅ |
| 05 | Cadaver | ✅ |
| 06 | Handler | ✅ |
| 07 | Meterpreter | ✅ |
| 08 | PostgreSQL & Metasploit Database | ✅ |
| 09 | Complete Attack Chain | ✅ |
| 10 | Mentor Challenge | ✅ |
| 11 | Quick Revision | ✅ |

> **Note:** The status icons represent the planned structure of this episode. They can be updated as the handbook grows.

---

# 🧠 Penetration Tester Mindset

One of the biggest mistakes beginners make is trying to memorize commands.

Professional penetration testers do not memorize random commands.

They understand the attack methodology.

When the methodology is clear, choosing the correct tool becomes much easier.

Throughout this handbook, every chapter answers four important questions:

1. **What is this?**
2. **Why is it used?**
3. **How does it work internally?**
4. **Where does it fit into the attack chain?**

---

# 🗺️ Episode Learning Flow

```text
Reconnaissance
        │
        ▼
Discover WebDAV
        │
        ▼
Test Upload Permissions
        │
        ▼
Generate Payload
        │
        ▼
Upload Payload
        │
        ▼
Start Handler
        │
        ▼
Receive Reverse Connection
        │
        ▼
Meterpreter Session
        │
        ▼
Post Exploitation
```

Every topic in this episode follows this exact attack flow.

---

# 🛠️ Skills You Will Gain

After completing Episode 01, you will be able to:

- Analyze exposed web services.
- Identify insecure WebDAV implementations.
- Understand payload generation.
- Configure reverse shell listeners.
- Gain remote access during a penetration test.
- Understand the purpose of Meterpreter.
- Follow a complete exploitation workflow from start to finish.

---

# 📖 Prerequisites

Before starting this episode, it is recommended that you understand:

- Basic Networking
- HTTP Protocol
- Web Servers
- Basic Linux Commands
- Basic Metasploit Navigation

---

# ⭐ Mentor's Golden Rule

> **Never ask "Which command should I use?"**

Instead ask:

> **"What is my objective at this stage of the attack?"**

Once you know your objective, choosing the correct tool becomes much easier.

---

# 📈 Episode Progress

```text
Repository Foundation      ✅
Episode Introduction       ✅
WebDAV                     ⏳
davtest                    ⏳
msfvenom                   ⏳
Reverse Shell              ⏳
Cadaver                    ⏳
Handler                    ⏳
Meterpreter                ⏳
Attack Chain               ⏳
Mentor Challenge           ⏳
Quick Revision             ⏳
```

This checklist will be updated as each chapter is completed.

---

# 🚀 What Comes Next?

The next chapter introduces **WebDAV**, the technology that starts the entire attack chain.

Rather than simply defining WebDAV, we will explore:

- Why Microsoft created it.
- How it extends HTTP.
- Why penetration testers are interested in it.
- How attackers identify insecure WebDAV configurations.
- How WebDAV becomes the first step toward remote code execution.

---

## 📘 Continue Learning

➡️ Next Chapter: **01-WebDAV.md**
