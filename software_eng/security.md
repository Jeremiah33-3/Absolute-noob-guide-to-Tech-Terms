# Authentication
## Session vs JWT

Video [Guide](https://youtu.be/fyTxwIa-1U0?si=DjyelRQfaYYjaSMa).

Session vs. JWT: The Core Difference
The fundamental difference lies in where the "state" (user login status) is stored:

Session (Stateful): The server keeps a record of the logged-in user (usually in memory or a database). The client is given a simple "ID card" (Session ID) that matches that record.

JWT (Stateless): The server keeps no record. The client is given a signed "passport" (JWT) containing all their details. The server trusts the passport because it signed it, not because it remembers it.

| Feature        | Session-Based Authentication | JWT (JSON Web Token) |
|----------------|------------------------------|----------------------|
| State          | Stateful: Server remembers active sessions. | Stateless: Server does not track active tokens. |
| Storage (Client) | Cookie (Sent automatically). | Local Storage or Cookie (Sent in Header). |
| Storage (Server) | Required: Stored in Memory, Redis, or DB. | None: Only the signature secret is stored. |
| Revocation     | Immediate: Server deletes the session data. | Difficult: Token is valid until expiration. |
| Scalability    | Harder: Requires sticky sessions or shared DB. | Easier: Works across multiple servers instantly. |
| Bandwidth      | Low: Cookie is tiny (just an ID). | High: Token contains data (Claims), making it larger. |
| Best For       | Traditional Monolithic Web Apps (e.g., Banking). | Microservices, SPAs, Mobile Apps. |

### Key Comparison

**1. The Workflow**

Session:

> 1. User logs in.
> 2. Server creates a session in its database: { "id": "xyz", "user": "Alice" }.
> 3. Server sends the ID "xyz" to the browser as a Cookie.
> 4. Next Request: Browser sends cookie "xyz". Server looks up "xyz" in the DB to find "Alice".

JWT:

> 1. User logs in.
> 2. Server creates a JSON object: { "user": "Alice", "role": "admin" }.
> 3. Server signs it mathematically using a secret key and sends the full token to the client.
> 4. Next Request: Client sends the token. Server verifies the signature math. If the math checks out, it trusts the data. No DB lookup required.

**2. Scalability**

Session: If you have 5 servers, they all need access to the same session data (usually via Redis). If that central database goes down, no one can log in.

JWT: Because the token verifies itself, any server with the secret key can authenticate the user. You can add 100 new servers without worrying about syncing session data.

**3. Security & Revocation (The "Kick-Out" Problem)**

Session: If you want to ban a user or force a logout (e.g., "Log out of all devices"), you simply delete their session ID from the server. Access stops immediately.

JWT: You cannot "delete" a JWT that is already on a user's phone. It remains valid until it expires (often 15–60 minutes).
- Workaround: To revoke JWTs, you must implement a "Blocklist" (storing invalid tokens), which accidentally re-introduces the statefulness/database you were trying to avoid.

**4. Vulnerabilities**

Session: Vulnerable to CSRF (Cross-Site Request Forgery) because cookies are sent automatically. You need anti-CSRF tokens to prevent this.

JWT: If stored in localStorage, it is vulnerable to XSS (Cross-Site Scripting). If malicious JS runs on your page, it can steal the token.

Best Practice: Store JWTs in HttpOnly Cookies to prevent XSS, effectively treating them like signed sessions.

### Which one should you use?

Use Sessions if:
- You are building a traditional server-side rendered app (Django, Rails, PHP, ASP.NET).
- Immediate revocation is critical (e.g., Banking apps, Admin panels) where you need to ban users instantly.
- Your app runs on a single server or you have a simple Redis setup.

Use JWT if:
- You are building a Single Page App (React/Vue/Angular) talking to an API.
- You have a Mobile App (Cookies are hard to manage in native mobile apps).
- You are using Microservices (Passing a JWT between services is faster than every service checking a central DB).

# API

Video [Guide](https://www.youtube.com/watch?v=FsB_nRGdeLs).
