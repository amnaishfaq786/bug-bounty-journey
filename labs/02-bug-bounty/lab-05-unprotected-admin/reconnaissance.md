# Reconnaissance

## Objective

Identify any hidden or sensitive functionality before attempting to test the application.

---

## Initial Observation

The lab description suggested that an administrator panel existed but did not specify its location.

Instead of guessing URLs, reconnaissance was performed.

---

## Step 1 – Check robots.txt

Visited:

/robots.txt

Response:

```
User-agent: *
Disallow: /administrator-panel
```

---

## Analysis

The `robots.txt` file instructs search engines not to crawl the administrator panel.

This is **not** a security mechanism.

Anyone who knows the URL can still access it.

---

## Step 2 – Verify the Endpoint

Visited:

/administrator-panel

Observation:

The administrator panel was accessible without authentication.

No login page was displayed.

No authorization checks were enforced.

---

## Result

Successfully identified an exposed administrator interface through reconnaissance.

This led directly to the vulnerability.
