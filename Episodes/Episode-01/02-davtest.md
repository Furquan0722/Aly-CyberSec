---
Title: davtest
Episode: 01
Category: WebDAV Enumeration
Difficulty: ⭐⭐☆☆☆
Reading Time: 18 Minutes
Revision Time: 6 Minutes
Prerequisites:
  - Understanding WebDAV
Related Topics:
  - WebDAV
  - Cadaver
  - msfvenom
Tags:
  - WebDAV
  - davtest
  - Enumeration
Version: 1.0
---

# 🧪 Chapter 02 — Discovering WebDAV Capabilities with davtest

> *"Never upload a real payload before understanding what the server allows."*

---

# 🌍 Real-World Scenario

You have identified that the target web server has **WebDAV enabled**.

Now the next question is:

Can this server accept file uploads?

Even more importantly...

Can it accept **executable files** like `.asp`?

Uploading a real payload without knowing the answer is risky and unprofessional.

Instead, penetration testers perform **safe capability testing**.

This is exactly why the **davtest** tool exists.

---

# 🎯 Learning Objectives

After completing this chapter you will understand:

- What davtest is
- Why penetration testers use davtest
- How davtest works internally
- How davtest tests upload permissions
- Why davtest is used before Cadaver
- How davtest fits into the attack chain

---

# 📖 What is davtest?

**davtest** is a WebDAV enumeration tool.

It is designed to safely test the capabilities of a WebDAV server.

Instead of uploading a malicious payload, it uploads small test files with different extensions to determine:

- Which file types are accepted
- Which file types are rejected
- Which uploaded files can be executed
- Which uploaded files are only stored

This allows a penetration tester to understand the target before attempting exploitation.

---

# 🤔 Why Do We Use davtest?

Imagine you immediately upload:

```
shell.asp
```

What if:

- `.asp` uploads are blocked?
- Authentication is required?
- The file is stored but never executed?

You would waste time and potentially create unnecessary noise on the target.

Instead, **davtest** answers these questions safely.

It helps you choose the correct payload later.

---

# 🧠 Pentester Mindset

Professional penetration testers never assume.

They verify.

Instead of asking:

> "Can I upload my shell?"

They ask:

> "What does the server actually allow me to upload?"

That small difference is what separates methodology from guesswork.

---

# ⚙️ Behind the Scenes

Internally, davtest performs several actions automatically:

1. Connects to the WebDAV service.
2. Uploads harmless test files with different extensions.
3. Attempts to access those files.
4. Checks whether the files execute or simply download.
5. Deletes the test files (when possible).
6. Generates a report of the server's behavior.

The tool is performing reconnaissance—not exploitation.

---

# 💻 Practical Lab

## 🎯 Objective

Determine which file extensions the WebDAV server accepts and whether uploaded files can execute.

---

## 🧪 Lab Environment

**Attacker**

- Kali Linux

**Target**

- Windows Server
- IIS
- WebDAV Enabled

---

<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/b997fea2-0a5d-4a81-8289-1746377be964" />


## Step 1 — Verify the WebDAV URL

Before running davtest, ensure you know the correct WebDAV directory.

Example:

```
http://TARGET/webdav/
```

---

## Step 2 — Run davtest

```bash
davtest -url http://TARGET/webdav
```

---

## 🔍 Command Breakdown

| Option | Meaning |
|---------|---------|
| davtest | Launch the tool |
| -url | Specifies the WebDAV target URL |

---

## 📤 Expected Output

A successful scan may produce results similar to:

```
Testing PUT functionality...
Uploading test files...
Checking execution...
```

Eventually you may see something like:

```
.asp    SUCCESS
.txt    SUCCESS
.cgi    FAIL
.php    FAIL
```

---

## 🧠 What Does This Mean?

Suppose the output shows:

```
.asp SUCCESS
```

This tells us:

✅ The server accepts ASP uploads.

However...

This **does not automatically mean code execution**.

The next step is to determine whether the uploaded ASP file actually executes.

---

## ⚠️ Common Errors

### Connection Refused

Possible causes:

- Incorrect URL
- WebDAV disabled
- Firewall blocking access

---

### Authentication Required

The server requires valid credentials before testing uploads.

---

### Upload Failed

Possible reasons:

- Write permissions disabled
- WebDAV configured as read-only
- Incorrect directory

---

# 🔗 Attack Chain Position

```text
Reconnaissance
        │
        ▼
Discover WebDAV
        │
        ▼
✅ davtest
        │
        ▼
Identify Allowed Extensions
        │
        ▼
Generate Payload
```

davtest helps us answer one critical question:

**Which payload should we create?**

---

# ⭐ Golden Rules

⭐ Never upload a real payload before testing permissions.

⭐ davtest is an enumeration tool, not an exploitation tool.

⭐ Successful upload does not guarantee code execution.

⭐ Always verify results before moving forward.

---

# ❌ Common Beginner Mistakes

❌ Using Cadaver immediately.

✔ Correct:

First understand what the server accepts.

---

❌ Assuming `.asp SUCCESS` means Remote Code Execution.

✔ Correct:

It only confirms upload capability. Execution must still be verified.

---

# 💡 Memory Trick

Imagine an airport.

Before boarding, security checks what items are allowed.

davtest acts like airport security.

It tells you what can pass through.

Only after knowing the rules do you prepare the correct "package."

---

# 🎯 eJPT Focus

Remember:

- Purpose of davtest
- Relationship with WebDAV
- Why enumeration comes before exploitation
- Difference between upload success and execution success

---

# 🔥 OSCP Insight

Modern environments may restrict many file types.

A penetration tester should never rely on a single extension.

Instead, enumerate, adapt, and test based on the target's behavior.

---

# 📋 Chapter Summary

Today you learned:

✅ What davtest is

✅ Why it is used

✅ How it works internally

✅ How to test upload permissions

✅ Why enumeration always comes before exploitation

---

# 🏆 Mentor Challenge

Imagine davtest reports:

```
.txt SUCCESS
.asp FAIL
.php FAIL
```

Question:

Should you immediately conclude that the target cannot be exploited?

Or are there additional avenues you should investigate?

Think like a penetration tester before answering.

---

## 🔗 Continue Learning

**Previous:** Chapter 01 – WebDAV

**Next:** Chapter 03 – msfvenom
