---
Title: WebDAV
Episode: 01
Category: Web Technologies
Difficulty: ⭐⭐☆☆☆
Reading Time: 15 Minutes
Revision Time: 5 Minutes
Prerequisites:
  - Basic HTTP
  - Basic Web Servers
Related Topics:
  - davtest
  - Cadaver
  - msfvenom
Tags:
  - WebDAV
  - IIS
  - HTTP
Version: 1.0
---

# 🌐 Chapter 01 — Understanding WebDAV

> *"A penetration tester never attacks a service before understanding why it exists."*

---

# 🌍 Real-World Scenario

Imagine you are hired to perform an internal penetration test for a company.

During reconnaissance, you discover a Microsoft IIS web server.

While enumerating the web server, one result immediately catches your attention.

```
WebDAV Enabled
```

Most people would ignore it.

A penetration tester immediately starts asking questions.

- What exactly is WebDAV?
- Why is it enabled?
- Can users upload files?
- Does it require authentication?
- Can uploaded files be executed?
- Could this become my entry point into the system?

This chapter answers the very first question.

**What is WebDAV?**

---

# 🎯 Learning Objectives

After completing this chapter you will understand:

- What WebDAV is
- Why WebDAV was created
- How WebDAV extends HTTP
- Why penetration testers investigate WebDAV
- Why WebDAV itself does NOT execute code
- How WebDAV fits into the attack chain

---

# 📖 What is WebDAV?

**WebDAV** stands for:

> **Web Distributed Authoring and Versioning**

It is an extension of the **HTTP protocol** that allows users to remotely manage files stored on a web server.

Unlike a normal website, WebDAV allows users to:

- Upload files
- Download files
- Rename files
- Move files
- Delete files
- Edit files remotely

Think of WebDAV as converting a normal website into a shared network folder that can be accessed through HTTP.

---

# 🤔 Why Was WebDAV Created?

Before WebDAV, users mainly transferred files using FTP.

Although FTP worked well, it had several limitations.

Organizations wanted employees to:

- Collaborate remotely
- Edit documents online
- Upload files directly through HTTP
- Manage files without using FTP

To solve this problem, WebDAV was introduced.

Its goal was productivity—not security testing.

However, when WebDAV is misconfigured, it can become an attractive target for attackers.

---

# 🏗️ How Does WebDAV Work?

Normal HTTP mainly supports methods like:

- GET
- POST
- HEAD

WebDAV extends HTTP by introducing additional methods such as:

| Method | Purpose |
|---------|---------|
| PUT | Upload a file |
| DELETE | Remove a file |
| COPY | Copy a file |
| MOVE | Move or rename a file |
| PROPFIND | Retrieve file properties |
| MKCOL | Create a directory |
| LOCK | Lock a file |
| UNLOCK | Unlock a file |

These methods transform a web server into a remote file management system.

---

# ⚙️ Behind the Scenes

This is one of the most misunderstood concepts.

Many beginners believe:

> "WebDAV executes uploaded files."

❌ Incorrect.

WebDAV only **transfers and manages files**.

The execution depends on the web server.

For example:

1. You upload `shell.asp` using WebDAV.
2. The file is stored on the server.
3. IIS receives a request for `shell.asp`.
4. IIS recognizes `.asp` as executable.
5. IIS executes the ASP code.
6. The payload runs.

Notice something important.

**WebDAV never executes the file.**

It only stores it.

---

# 🧠 Pentester Mindset

When you discover WebDAV during reconnaissance, your first thought should **NOT** be:

> "Let's upload a payload."

Instead, think like a professional.

Ask yourself:

- Is uploading allowed?
- Which extensions are accepted?
- Is authentication required?
- Can uploaded files be accessed?
- Can they actually be executed?

These questions guide your next steps.

Good penetration testers investigate before they exploit.

---

# 💻 Practical Lab

## 🎯 Lab Objective

Identify whether a target exposes WebDAV and understand why it may become an attack surface.

---

## 🧪 Lab Environment

**Attacker**

- Kali Linux

**Target**

- Windows Server
- Microsoft IIS
- WebDAV Enabled

---

## Step 1 — Identify the Web Server

```bash
nmap -sV TARGET_IP
```

### Why are we doing this?

Before attacking anything, we must identify:

- Running services
- Server software
- Open ports

This tells us whether IIS is running.

---

### Expected Output

You may observe something similar to:

```
80/tcp open http Microsoft IIS
```

This tells us the target is using Microsoft IIS.

It does **NOT** confirm WebDAV yet.

---

## Step 2 — Look for WebDAV

Once IIS is discovered, the next objective is determining whether WebDAV is enabled.

At this point, **do not upload anything**.

The next chapter introduces **davtest**, the tool that safely checks upload capabilities.

---

# 📊 Attack Flow

```text
Reconnaissance
        │
        ▼
Discover IIS
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
Receive Reverse Shell
```

---

# 🔬 Internal Working

Behind the scenes, the process looks like this:

```
Browser
      │
      ▼
HTTP Request
      │
      ▼
WebDAV
      │
      ▼
Stores File
      │
      ▼
Microsoft IIS
      │
      ▼
Processes ASP
      │
      ▼
Returns Response
```

Understanding this architecture explains why WebDAV alone cannot compromise a server.

The web server configuration determines what happens after upload.

---

# ⭐ Golden Rules

⭐ WebDAV manages files.

⭐ IIS executes ASP files.

⭐ Never assume file upload means code execution.

⭐ Always enumerate before exploiting.

⭐ Understanding methodology is more valuable than memorizing commands.

---

# ❌ Common Beginner Mistakes

### Mistake 1

Immediately uploading a payload.

✔ Correct Approach

First determine whether uploads are even allowed.

---

### Mistake 2

Thinking WebDAV executes ASP files.

✔ Correct Approach

IIS executes ASP files.

---

### Mistake 3

Ignoring WebDAV during reconnaissance.

✔ Correct Approach

Always investigate exposed file management services.

---

# 💡 Memory Trick

Imagine a company office.

📦 **WebDAV = Reception Desk**

The receptionist accepts your package and stores it.

👨‍💼 **IIS = Office Employee**

The employee opens and processes the package.

The receptionist never processes the package.

Likewise,

WebDAV stores files.

IIS executes files.

---

# 🎯 eJPT Exam Focus

For the eJPT exam, remember these concepts:

- Definition of WebDAV
- Purpose of WebDAV
- Relationship between WebDAV and HTTP
- Why attackers enumerate WebDAV
- Difference between uploading and executing a file

Understanding these ideas is more important than memorizing definitions.

---

# 🔥 OSCP Professional Insight

In real-world environments, discovering WebDAV is only the beginning.

A successful attack depends on several factors:

- Authentication
- File permissions
- Allowed extensions
- Web server configuration
- Execution permissions

Professional penetration testers verify each assumption instead of relying on luck.

---

# 📋 Chapter Summary

Today you learned:

✅ What WebDAV is

✅ Why it was created

✅ How it extends HTTP

✅ Why penetration testers investigate it

✅ Why WebDAV does not execute uploaded files

✅ Where WebDAV fits into an attack chain

---

# 🏆 Mentor Challenge

Imagine you discover a WebDAV server.

It allows file uploads.

However, every uploaded ASP file downloads instead of executing.

**Question:**

Why might this happen?

Think before reading the next chapter.

The answer depends on understanding **the relationship between WebDAV and IIS**, not WebDAV alone.

---

## 🔗 Continue Learning

**Previous:** Episode 01 Introduction

**Next:** Chapter 02 — davtest
