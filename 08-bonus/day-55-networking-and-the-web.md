# Day 55: BONUS: Networking and the Web

- [ ] Coding problem done
- [ ] Concepts read and notes written
- [ ] Check answered out loud

**Time plan (about 2 hours):** 45 min coding · 60 min concepts · 15 min out-loud check

---

## Part 1: Coding problem (45 min)

**Problem:** Pacific Atlantic Water Flow (Graph DFS, Medium)

1. Spend up to 25 minutes on your own first.
2. Then read the approach below and code it again from scratch, without looking.

**First idea (works, but slower):** From every cell, search whether water reaches both oceans: O((m·n)²).

**Best approach:** Reverse it: DFS inward from each ocean's border to cells of equal or greater height. Answer = cells reached from both.

```python
def pacificAtlantic(h):
    m, n = len(h), len(h[0])
    def dfs(r, c, seen):
        seen.add((r, c))
        for dr, dc in ((1,0),(-1,0),(0,1),(0,-1)):
            nr, nc = r + dr, c + dc
            if 0 <= nr < m and 0 <= nc < n and (nr, nc) not in seen and h[nr][nc] >= h[r][c]:
                dfs(nr, nc, seen)
    pac, atl = set(), set()
    for i in range(m):
        dfs(i, 0, pac); dfs(i, n - 1, atl)
    for j in range(n):
        dfs(0, j, pac); dfs(m - 1, j, atl)
    return [list(x) for x in pac & atl]
```

---

## Part 2: Concepts (60 min)

### Real-world scenario

'What happens when you type a URL into a browser?' is a classic question. You walk through DNS lookup, a TCP connection, a TLS handshake, the HTTP request, the server response and the browser rendering the page.

### What to understand

**DNS**  
Translates a domain to an IP address via resolvers and caches.

**TCP vs UDP**  
TCP: reliable, ordered, connection-based (web, APIs). UDP: fast, no guarantees (video calls, gaming).

**HTTP and HTTPS**  
Request/response protocol; HTTPS adds TLS encryption with certificates.

**HTTP/1.1, 2, 3**  
HTTP/2 multiplexes many requests on one connection; HTTP/3 runs over QUIC (UDP).

**Cookies, sessions, tokens**  
Sessions store state server-side; JWTs carry signed claims client-side. OAuth for delegated login.

**CORS**  
Browser rule controlling which other origins can call your API.

### Interview questions

Try answering each one out loud before reading the answer.

**Q1. What happens when you type a URL?**  
DNS → TCP → TLS → HTTP request → server → response → render.

**Q2. TCP vs UDP?**  
TCP is reliable and ordered; UDP is faster without guarantees.

**Q3. What does HTTPS protect?**  
Encrypts data in transit and verifies the server's identity.

**Q4. What is a JWT?**  
A signed token containing user claims, checked without a database lookup.

---

## Part 3: Out-loud check (15 min)

> Answer 'what happens when you type a URL' in 2 minutes.

Tick the box at the top only when you can do this without notes.

---

## Quick review

- DNS → TCP → TLS → HTTP
- TCP reliable; UDP fast
- HTTPS = TLS encryption
- JWT = signed claims
- CORS = cross-origin rules
