
# Inbäddning av Marvify 3D-visare: Guide för COEP & COOP-inställningar

För att säkert bädda in **Marvify 3D-visaren** på er webbplats måste er webbserver skicka följande HTTP-säkerhetsrubriker:

```http
Cross-Origin-Embedder-Policy: require-corp
Cross-Origin-Opener-Policy: same-origin
```

Dessa rubriker krävs för att visaren ska fungera korrekt i moderna webbläsare. Utan dem kan visningen blockeras.

---

## ✅ Kompatibilitetsmatris

| Plattform                        | Går det att ställa in rubriker? | Stöd för inbäddning | Kommentar |
|----------------------------------|----------------------------------|----------------------|-----------|
| Apache (egen server)             | ✅ Ja                            | ✅ Fullt stöd        | Redigera `.htaccess` eller serverinställningar |
| Nginx (egen server)              | ✅ Ja                            | ✅ Fullt stöd        | Kräver åtkomst till Nginx-konfigurationsfilen |
| Node.js (Express)                | ✅ Ja                            | ✅ Fullt stöd        | Ändra serverkod med Express-mellanlager |
| Netlify                          | ✅ Ja                            | ✅ Fullt stöd        | Lägg till i filen `_headers` i projektroten |
| Cloudflare Pages / Workers       | ✅ Ja                            | ✅ Fullt stöd        | Använd `_headers`-fil eller Workers-script |
| Vercel                           | ✅ Ja                            | ✅ Fullt stöd        | Lägg till i `vercel.json`-konfigurationen |
| WordPress (egen host)            | ✅ Ja                            | ✅ Fullt stöd        | Som Apache/Nginx beroende på hostingleverantör |
| Firebase Hosting                 | ✅ Ja                            | ✅ Fullt stöd        | Redigera `firebase.json` |
| WordPress.com (hostad)           | ❌ Nej                           | ❌ Inget stöd        | Ingen åtkomst till serverinställningar |
| Wix                              | ❌ Nej                           | ❌ Inget stöd        | Begränsad plattform utan serverkontroll |
| Squarespace                      | ❌ Nej                           | ❌ Inget stöd        | Detsamma som ovan |
| Shopify                          | ❌ Nej                           | ❌ Inget stöd        | Ingen möjlighet att ändra headers |
| Webflow                          | ❌ Nej                           | ❌ Inget stöd        | Endast begränsat stöd för anpassad kod |


---

## Så här ställer du in säkerhetsrubrikerna

### Apache (.htaccess)

För mer hjälp: [Apache .htaccess Docs](https://httpd.apache.org/docs/current/howto/htaccess.html)

```apache
<IfModule mod_headers.c>
  Header set Cross-Origin-Embedder-Policy "require-corp"
  Header set Cross-Origin-Opener-Policy "same-origin"
</IfModule>
```

---

### Nginx

👉 För mer hjälp: [Nginx Headers Module](https://nginx.org/en/docs/http/ngx_http_headers_module.html)

```nginx
add_header Cross-Origin-Embedder-Policy "require-corp" always;
add_header Cross-Origin-Opener-Policy "same-origin" always;
```

🔁 Glöm inte att starta om Nginx efter ändringen.

---

### Node.js (Express)

👉 För mer hjälp: [Express API Docs](https://expressjs.com/en/4x/api.html#res.set)

```js
app.use((req, res, next) => {
  res.setHeader("Cross-Origin-Embedder-Policy", "require-corp");
  res.setHeader("Cross-Origin-Opener-Policy", "same-origin");
  next();
});
```

🔁 Starta om din server efter ändring.

---

### Netlify

👉 För mer hjälp: [Netlify Headers Docs](https://docs.netlify.com/routing/headers/)

Skapa eller redigera en `_headers`-fil i projektets rot:

```
/*
  Cross-Origin-Embedder-Policy: require-corp
  Cross-Origin-Opener-Policy: same-origin
```

---

### Cloudflare Pages

👉 För mer hjälp: [Cloudflare Pages Headers](https://developers.cloudflare.com/pages/platform/headers/)

Använd en `_headers`-fil:

```
/*
  Cross-Origin-Embedder-Policy: require-corp
  Cross-Origin-Opener-Policy: same-origin
```

**Alternativ: Cloudflare Worker**

```js
addEventListener("fetch", event => {
  event.respondWith(handleRequest(event.request))
})

async function handleRequest(request) {
  const response = await fetch(request)
  const newHeaders = new Headers(response.headers)
  newHeaders.set("Cross-Origin-Embedder-Policy", "require-corp")
  newHeaders.set("Cross-Origin-Opener-Policy", "same-origin")
  return new Response(response.body, {
    status: response.status,
    statusText: response.statusText,
    headers: newHeaders,
  })
}
```

---

### Vercel

👉 För mer hjälp: [Vercel Headers Docs](https://vercel.com/docs/projects/project-configuration#headers)

Lägg till i `vercel.json`:

```json
{
  "headers": [
    {
      "source": "/(.*)",
      "headers": [
        {
          "key": "Cross-Origin-Embedder-Policy",
          "value": "require-corp"
        },
        {
          "key": "Cross-Origin-Opener-Policy",
          "value": "same-origin"
        }
      ]
    }
  ]
}
```

---

### Firebase Hosting

👉 För mer hjälp: [Firebase Hosting Headers](https://firebase.google.com/docs/hosting/full-config#headers)

Redigera `firebase.json`:

```json
{
  "hosting": {
    "headers": [
      {
        "source": "**",
        "headers": [
          {
            "key": "Cross-Origin-Embedder-Policy",
            "value": "require-corp"
          },
          {
            "key": "Cross-Origin-Opener-Policy",
            "value": "same-origin"
          }
        ]
      }
    ]
  }
}
```

---

## ❌ Plattformar som **inte** stöder inbäddning

Följande plattformar tillåter **inte** att de nödvändiga säkerhetsrubrikerna sätts, vilket gör att `<iframe>`-inbäddning **inte** fungerar:

- WordPress.com (hostad version)
- Wix
- Squarespace
- Shopify
- Webflow

---

## 🧩 Alternativ lösning: Öppna visaren i nytt fönster

Om du använder en plattform som inte stöder COEP/COOP kan du ändå länka till visaren utan att förlora besökaren:

### Lösning 1 – Länk eller knapp

```html
<a href="https://v.marvify.io/?m=cHJhbGluZXM" target="_blank" rel="noopener">
  Visa i 3D
</a>
```

### Lösning 2 – Popup-fönster

```html
<button onclick="window.open('https://v.marvify.io/?m=cHJhbGluZXM', 'popup', 'width=800,height=600'); return false;">
  Öppna 3D-visning
</button>
```

---

