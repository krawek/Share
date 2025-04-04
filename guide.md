# Marvify 3D Viewer  
## Guide för användning på er webbplats och i sociala medier

---

## Vad är Marvify FOTO-3D?

Marvify erbjuder en interaktiv visare som gör det möjligt för er att visa upp era FOTO-3D produkter digitalt – på ett engagerande och flexibelt sätt. Med en enkel länk kan ni låta era kunder rotera, zooma och utforska produkten i detalj, direkt i webbläsaren. Det fungerar lika bra på produkt- och kampanjsidor som i annonser, bloggar, sociala medier och e-commerce.

---

## Hur man redigerar HTML

Vissa av exemplen i den här guiden kräver att ni kan lägga in en länk eller ett HTML-element på er webbplats eller e-handelsplattform.  
Om ni är osäkra – klicka här för en enkel introduktion:  
**[Läs en guide om hur man redigerar HTML](#)**

---

## 💬 Exempel på hur ni kan använda 3D-visaren

### "Vi vill länka till vår FOTO-3D chipspåse på hemsidan!"

**Lösning – textlänk på webbsida eller i artikel:**
```HTML
<a href="https://v.marvify.io/?m=Y2hpcHNhbHQ" target="_blank">Se påsen i 3D</a>
```
---

### "Vi vill lägga en snygg knapp på produktsidan för vår FOTO-3D Pizza!"

**Lösning – länk stylad som knapp:**
```HTML
<a href="https://v.marvify.io/?m=Y2hpcHNhbHQ" class="button" target="_blank">Se i 3D</a>
```
Ni kan använda er webbplats eller e-handelsplattform för att formatera länken som en knapp, så att den smälter in i er design.

---

### "Kan man klicka på bilden av lakritsen på min hemsida för att öppna FOTO-3D?"

**Lösning – klickbar bild med länk:**
```HTML
<a href="https://v.marvify.io/?m=bGFrcml0cw==" target="_blank">
  <img src="lakritsbild.jpg" alt="Se lakrits i 3D" />
</a>
```
---

### "Vi vill visa våra FOTO-3D energibars i en popup istället för ny flik!"

**Lösning – öppna visaren i popupfönster:**

Ni kan använda både en **knapp** eller en **länk** för att öppna popupen.

Exempel med knapp:
```HTML
<button onclick="open3DViewer()">Se produkten i 3D</button>
```
Exempel med länk:
```HTML
<a href="#" onclick="open3DViewer()">Öppna 3D-visning</a>
```
Javascript:
```JS
<script>
function open3DViewer() {
  window.open("https://v.marvify.io/?m=bnV0YmFyMTA", "_blank", "width=800,height=600");
}
</script>
```
---

### "Vi ska trycka menyer – kan vi använda FOTO-3D?"

**Lösning – skapa en QR-kod med er visningslänk:**  
Exempel på QR-kodgenerator: [länk]

Länk att använda:  
https://v.marvify.io/?m=Y2hvY2tib3gyMw==

Textförslag:  
*Skanna för att se vår produkt i 3D*

---

### "Vi vill bädda in visningen av våra FOTO-3D praliner direkt på hemsidan!"

**Lösning – inbäddning med iframe:**
```HTML
<iframe src="https://v.marvify.io/?m=cHJhbGluZXM" width="100%" height="500px" style="border:none;"></iframe>
```
**Notera:**  
För att visaren ska fungera krävs att följande två säkerhetsinställningar är aktiverade i er webb-server:
```
Cross-Origin-Embedder-Policy: require-corp  
Cross-Origin-Opener-Policy: same-origin
```
Om dessa inte finns kommer innehåll i visaren att blockeras i webbläsaren.

**Exempel på guider för vanliga plattformar:**

- Apache [länk till guide]  
- Nginx [länk till guide]  
- Node.js (Express) [länk till guide]  
- Netlify [länk till guide]  
- Cloudflare Pages / Workers [länk till guide]

---


## 🌐 Så kan ni använda visaren i sociala medier

Här visar vi hur ni kan använda er unika Marvify-länk i sociala medier för att marknadsföra era produkter. Ni får konkreta exempel på hur ni kan publicera länken i vanliga inlägg, stories och annonser – oavsett om det görs via ert eget konto, en influencer eller en ambassadör.

---

### Instagram

#### Vanligt konto, influencer eller ambassadör

**Lösning – Länk i bio:**

Ni kan lägga länken till er visare i profilen (bio) och därefter skapa ett vanligt inlägg i flödet där ni hänvisar till den. Det fungerar oavsett om inlägget kommer från er själva, en influencer eller en ambassadör.

> Jag blev helt kär i de här nya småkakorna från @SweetCrave – och man kan faktiskt se hela förpackningen i 3D.  
> Klicka på länken i min bio!  
>

**Lösning – Story med Link Sticker:**

Skapa en Instagram Story med produktfoto och använd en **Link Sticker** för att lägga till klickbar länk direkt i bilden.

- Länk: https://v.marvify.io/?m=ZnJ1a3Rnb2Q=  
- Text på stickern: *"Se i 3D"*

---

#### Företagskonto & annonser

**Lösning – Annons med Meta Ads Manager:**

Med ett företagskonto kan ni skapa sponsrade inlägg i flödet eller Stories via Meta Ads Manager. Dessa annonser kan rikta sig mot specifika målgrupper och innehåller klickbara länkar.

Exempel:

Text:  
Snurra vår nya snackspåse i 3D – zooma, rotera och utforska innan du beställer.  
Länk: https://v.marvify.io/?m=aW5zdGFncjNkaQ==  
CTA-knapp: *Se mer*

---

### Facebook

#### Vanligt konto, influencer eller ambassadör

**Lösning – Vanligt inlägg i flödet:**

Ni (eller någon ni samarbetar med) kan skapa ett inlägg i ert personliga flöde med en kommentar och direktlänk till 3D-visningen.

> Jag testade de här nya jordnötssnacksen från @CrispyCrunch – så sjukt goda!  
> Man kan till och med snurra runt påsen i 3D.  
>  
> https://v.marvify.io/?m=Y3Jpc3B5ZGVsMA

---

#### Företagssida & annonser

**Lösning – Sponsrad annons eller vanligt inlägg:**

Ni kan publicera länken i ett vanligt inlägg från er företagssida, eller skapa en sponsrad annons som visas i målgruppens flöde.

Exempel:

Text:  
Ge bort något speciellt – snurra runt vår exklusiva pralinask i 3D.  
Länk: https://v.marvify.io/?m=cHJhbGluYXNrMg  
CTA-knapp: *Se i 3D*

---

### X (tidigare Twitter)

#### Vanligt konto, influencer eller ambassadör

**Lösning – Tweet i flödet:**

Ni kan skriva en vanlig tweet där ni lägger in länken till visningen. Det här fungerar också om en influencer eller ambassadör gör det åt er.

> Hur coolt är det att kunna snurra en godispåse i 3D?  
> Jag älskar den här från @SweetByte  
>  
> https://v.marvify.io/?m=c3dlZXRib3g1

---

#### Företagskonto & annonser

**Lösning – Promoted Tweet:**

Ni kan skapa en sponsrad tweet via ert företagskonto som visas för en utvald målgrupp.

> Upptäck vår limited edition nötmix – se hela förpackningen i 3D innan du klickar hem den.  
>  
> https://v.marvify.io/?m=bGltaXRub3Qz

---

### LinkedIn

#### Vanligt konto, influencer eller branschprofil

**Lösning – Personligt inlägg i flödet:**

Ni eller någon ni samarbetar med (t.ex. en branschperson, influencer eller anställd) kan lägga upp ett personligt inlägg i sitt flöde med en kommentar och länk.

> Otroligt hur mycket en 3D-visning kan höja kundupplevelsen.  
> Här är ett exempel på en produkt jag själv gillar – en lyxig chokladask i 3D.  
>  
> https://v.marvify.io/?m=Y2hvY2tleGVtcGxl

---

#### Företagssida & annonser

**Lösning – Sponsrat inlägg eller företagsinlägg i flödet:**

Ni kan använda er företagssida för att publicera ett organiskt inlägg eller en sponsrad annons riktad mot konsumenter eller återförsäljare.

> Vill ni visa era produkter på ett nytt sätt?  
> Så här ser vår ekologiska snackspåse ut – i 3D, direkt i webbläsaren.  
>  
> https://v.marvify.io/?m=ZWNvc3BhY2sx


---

## 🛒 Så kan ni använda 3D-visaren på e-handelsplattformar

På plattformar som WooCommerce, Shopify, Squarespace m.fl. kan ni enkelt länka till er Marvify-visning direkt från produktsidorna. Länken fungerar i alla webbläsare, även på mobil.

---

### "Vi har en WooCommerce-butik – hur lägger vi in vår 3D-länk till snackspåsen?"

**Lösning – Lägg in en länk direkt i produktbeskrivningen:**

I WooCommerce kan ni redigera produktens innehåll via WordPress admin. Lägg in en klickbar textlänk eller en knapp i beskrivningsfältet. Då ser kunden den direkt när de läser om produkten.
```HTML
<a href="https://v.marvify.io/?m=cHJvZHVrdGlk" target="_blank">Se produkten i 3D</a>
```
---

### "Vi använder Shopify – hur visar vi våra gelégodis i 3D?"

**Lösning – Lägg in länken i HTML-vyn i produktbeskrivningen:**

I Shopify går ni till adminpanelen → Produkter → Redigera produkt → Klicka på **“Visa HTML”** i beskrivningen. Där kan ni klistra in länken. Den syns sedan på produktsidan under produkttexten.
```HTML
<a href="https://v.marvify.io/?m=c2hvcGlmeXRlc3Q=" target="_blank">Utforska produkten i 3D</a>
```
---

### "Vi har Squarespace – kan vi lägga in 3D-visning på chokladbitarna?"

**Lösning – Länka direkt i produktbeskrivningen via editor:**

I Squarespace redigerar ni varje produktsida i editorn. Lägg till en vanlig länk i beskrivningsfältet. Den visas direkt för kunden under produktinformationen.
```HTML
<a href="https://v.marvify.io/?m=c3FzcGFjZXByb2Q=" target="_blank">Se produkten i 3D</a>
```
---

### "Vi bygger med Webflow – hur får vi med 3D-länken till nötmixen?"

**Lösning – Lägg till en extern länk i produktens layout:**

I Webflow använder ni designer-editorn för att lägga in knappar eller textlänkar. Sätt länken till er 3D-visning som en extern URL. Ni kan placera den precis där ni vill på sidan.

https://v.marvify.io/?m=d2ViZmxvd3Byb2Q=

---

### "Vi har vår butik i Magento – hur visar vi produkten i 3D där?"

**Lösning – Redigera produktbeskrivningen i adminpanelen:**

I Magento kan ni lägga till HTML direkt i produktbeskrivningsfältet via backend. Länken syns sedan tillsammans med övrig produktinfo.
```HTML
<a href="https://v.marvify.io/?m=bWFnZW50b3Byb2Q=" target="_blank">Visa i 3D</a>
```
---

### Tips

- Placera länken nära köpknappen eller produktbilden  
- Använd texter som *“Se i 3D”*, *“Utforska visuellt”* eller *“Snurra runt”*  
- Lägg gärna till en QR-kod i förpackning eller tryckt material
