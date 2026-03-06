# did:viewonwebsite — Deployment Package
## viewonwebsite.com — Sovereign Visual Integrity Root

**Architect:** Tamer Maher Eldebes  
**Authority:** Hardcoded Logic  
**Contact:** authority@hardcodedlogic.com  
**Jurisdiction:** Dubai, UAE  
**Version:** 1.0.0 — February 2026

---

## File Structure

```
did-viewonwebsite/
├── index.html                          # Main landing page (10/10)
├── .htaccess                           # Apache production config
├── nginx.conf                          # Nginx production config
├── .well-known/
│   ├── did-configuration.json          # DID configuration (W3C standard)
│   └── did.json                        # Root DID document
├── resolve/
│   └── index.html                      # Resolver endpoint documentation
└── spec/
    └── index.html                      # DID method specification v1.0
```

---

## Deployment Steps (Linode VPS)

### 1. Upload Files
```bash
scp -r did-viewonwebsite/* root@YOUR_LINODE_IP:/var/www/viewonwebsite.com/
```

### 2. Set Permissions
```bash
chmod -R 755 /var/www/viewonwebsite.com/
chown -R www-data:www-data /var/www/viewonwebsite.com/
```

### 3. Nginx Setup
```bash
cp nginx.conf /etc/nginx/sites-available/viewonwebsite.com
ln -s /etc/nginx/sites-available/viewonwebsite.com /etc/nginx/sites-enabled/
nginx -t
systemctl reload nginx
```

### 4. SSL Certificate (Let's Encrypt)
```bash
apt install certbot python3-certbot-nginx -y
certbot --nginx -d viewonwebsite.com -d www.viewonwebsite.com
```

### 5. Verify Live Endpoints
```
https://viewonwebsite.com/                              → Landing page
https://viewonwebsite.com/.well-known/did.json          → Root DID document
https://viewonwebsite.com/.well-known/did-configuration.json → DID config
https://viewonwebsite.com/resolve/                      → Resolver endpoint
https://viewonwebsite.com/spec/                         → DID specification
```

---

## W3C DID Registration

After deployment, submit the live resolver URL to Otto Mora (W3C DID Working Group):

1. Fork: https://github.com/w3c/did-extensions
2. Add `viewonwebsite` entry to `methods.json`
3. Submit pull request with live resolver URL

---

## The Physics Proof

| Condition | Authentication Gap | Visual Gap | Total Risk |
|-----------|-------------------|------------|------------|
| Without did:level5 | 3.33m | 6.67m | **10.00m fatal** |
| With did:level5 | 2.67cm | 0cm | **2.67cm safe** |

At 120 km/h — the difference between the child being hit and the child being safe is:
**Two domain names registered in Dubai.**

---

## Sovereign Stack

- `did:viewonwebsite` → viewonwebsite.com (this deployment)
- `did:verifiedcar` → verifiedcar.com (identity root)
- `did:level5` → Master certification (both roots simultaneously)

---

© 2026 Tamer Maher Eldebes · Hardcoded Logic · All Rights Reserved
