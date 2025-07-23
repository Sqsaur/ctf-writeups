# Confidential Document

**Category**: Sensitive Data Exposure  
**Difficulty**: 1.5  

### Description

This challenge required accessing confidential internal documents stored on the server.

---

### Solution

While exploring the `/ftp` directory (discovered during previous enumeration with Gobuster), I found a file named:

```
/ftp/acquisitions.md
```

Access to this file was not restricted, as it had a `.md` extension — one of the allowed file types.

I downloaded the file directly:

```
curl http://127.0.0.1:3000/ftp/acquisitions.md
```

The contents revealed confidential company plans for acquiring competitors, along with a clear warning:

> _"This document is confidential! Do not distribute!"_

---

**Challenge completed** by locating and accessing a sensitive `.md` document exposed in an unprotected directory.