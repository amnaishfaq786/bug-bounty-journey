# Lesson 1 – Anatomy of an HTTPS Request

## Objective

Understand what happens when a browser requests a webpage.

## Steps Observed

1. DNS resolved the domain.
2. TCP connection established.
3. TLS handshake completed.
4. HTTP GET request sent.
5. Server responded with HTTP 200.

## Key Findings

- HTTPS uses port 443.
- TLS encrypts the communication.
- The Host header identifies the requested website.
- Cloudflare acted as the edge server.
- The server returned HTML content.

## Commands Used

curl -I https://example.com

curl -v https://example.com
