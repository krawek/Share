## Loggingserver
- Minska avbrott  
- E-postnotifieringar  
- Tillåt cloud-skalning  

**Beskrivning av arbetet:**  
Just nu loggar våra träningsservrar till en lokal fil som överförs till vår NAS efter att ett dataset tränats färdigt. Detta fungerar i nuläget för lokal träning, men innebär att vi inte får någon varning vid kritiska eller störande fel förrän någon manuellt kontrollerar loggarna. Arbetsinsatsen består i att sätta upp en loggingserver som våra träningsskript kan skicka sina loggar till i realtid. Servern ska även kunna fånga upp fel och skicka e-postnotifieringar vid avbrott. Loggingfunktionen i sig är till största delen färdig, det som saknas är servern och notifieringsdelen.

**Motivering:**  
Ett loggingserver-system är avgörande för att vi ska kunna skala träningen av dataset i molnet. Utan det finns risken att misslyckade träningsjobb inte upptäcks förrän dataset saknas — vilket i vissa fall kan ske dagar senare. Vid samtidig träning av många dataset ökar denna risk. En loggingserver gör det möjligt att fånga fel i realtid och snabbt åtgärda dem, vilket minskar driftstörningar och förbättrar vår reaktionsförmåga. Det är en kritisk komponent för att säkerställa tillförlitligheten i vår träningspipeline både lokalt och i molnet.

---

## Viewer-dokumentation / Avslut 1.1
- Slutföra och dokumentera viewer-funktioner  

**Beskrivning av arbetet:**  
Vår 3D-viewer är i dagsläget funktionell men snabbt ihopslängd. Arbetet innebär att städa upp koden, dokumentera all funktionalitet, samt att standardisera layout och utseende där det är möjligt. En särskild fokuspunkt är att införa ett hårdkodat "default"-läge som visas när ingen config.json finns, vilket minskar behovet av manuell konfiguration. Vi bör även granska om något grundläggande saknas för att möta förväntningarna på en modern 3D-viewer-upplevelse. Detta arbete skapar en grund för snabbare vidareutveckling och enklare felsökning i framtiden.

**Motivering:**  
Utan dokumentation och en ren kodbas blir vidareutveckling och felsökning tidskrävande. Om en kund i framtiden efterfrågar ny funktionalitet kan det i nuläget ta en till två dagar bara för att sätta sig in i hur komponenterna fungerar. Genom att dokumentera ordentligt och standardisera gränssnittet reducerar vi manuell konfiguration och teknisk skuld. Ett korrekt implementerat default-läge kan minska tiden för efterbearbetning av splats med över 30 %, då config.json i nuläget är en av de mest tidskrävande momenten i vår pipeline.

---

## Projekthantering
- Löpande hantering av projekt  
- Kontinuerlig förbättring av processer och pipelines  

**Beskrivning av arbetet:**  
Eftersom detta är i ett tidigt skede går mycket tid åt till att instruera teamet samt att både jag och teamet lär oss arbeta effektivt i Monday.com. Processerna och pipelines är designade, men kommer förbättras och förfinas i takt med att vi lär oss mer om hur teamet föredrar att arbeta. Projekthanteringen är ett kontinuerligt arbete och kommer, när allt är på plats, att kräva minst en timme per dag för uppföljning genom stand-ups och spontana diskussioner med teammedlemmar. Tidsåtgången kommer att variera beroende på planering, omprioriteringar och om teamet stöter på hinder.

**Motivering:**  
Effektiv projekthantering är avgörande för att samordna teamets arbete och säkerställa att alla vet vad som ska göras och när. I takt med att arbetsflödet sätter sig kommer projekthanteringen vara nyckeln till att hålla både tempo och kvalitet uppe, samtidigt som vi minimerar risk för dubbelarbete, blockerare och felriktad utveckling. Det här är också fundamentet för att kunna skala teamet och våra processer på ett hållbart sätt.

---

## Träningsskript
- Minska antal splats  
- Logging  
- Dokumentation  

**Beskrivning av arbetet:**  
Vi håller på att implementera en funktion framtagen av Adam som gör det möjligt att reducera våra splats med cirka 50 % i filstorlek. Arbetet återstår att slutföra och testas grundligt innan det kan integreras i den skarpa träningspipen. Denna förbättring kräver att Nerfstudio körs flera gånger, vilket innebär en ökning av träningstiden med cirka 30–50 %. Parallellt behöver loggningen färdigställas och konfigureras för att kommunicera med en loggingserver. Dokumentation finns redan i viss mån, men behöver utökas för att täcka kodens struktur och logik i detalj.

**Motivering:**  
Att kunna generera betydligt mindre splats förbättrar slutanvändarens upplevelse markant — laddningstiden försvinner i princip vid snabba uppkopplingar. Det minskar också våra kostnader för datatrafik mot molnleverantören. Den ökade träningstiden motiverar horisontell skalning via molnet, vilket i sin tur kräver att vi har fungerande logging. Utan loggingserver är det omöjligt att upptäcka misslyckade träningsjobb förrän vi märker att dataset saknas i resultatmappen — ibland flera dagar senare om vi tränar flera samtidigt.  
Samtidigt har kodbasen blivit tillräckligt komplex för att göra framtida iterationer tidskrävande om vi inte dokumenterar bättre. Efter några månaders paus tar det i dagsläget flera dagar att återfå en fullständig förståelse för logiken i koden. En mer omfattande dokumentation kommer kraftigt minska den tidsförlusten.

---

### **Capture-skript**  
**Minska antal splats**  
**Logging**  
**Dokumentation**

---

**Beskrivning av arbetet:**  
Funktionaliteten för reducerad splatfilstorlek som implementerats i träningsskriptet behöver speglas i capture-verktygets UI, så att användaren som fotograferar våra objekt kan välja om den ska användas, hur många iterationer som ska köras och vid vilken procentuell nedskalning. Detta gör det möjligt att genom testning hitta ett standardvärde som ger mindre splats med bibehållen kvalitet, men också att finjustera inställningen för särskilt viktiga objekt eller VIP-kunder där högsta möjliga kvalitet prioriteras över snabbhet.

Utöver detta måste logging implementeras, helst med koppling till loggingservern. Det gör att vi kan fånga upp fel direkt och återgå till fotografering snabbt. Om fotografering sker offline (t.ex. i en mobil rigg som en bil) måste loggar buffras lokalt och skickas när anslutning finns igen. En ännu bättre lösning än att endast buffra loggar vore att också visa felmeddelanden tydligt för användaren direkt i offline-läget, så att de kan agera på eventuella problem i stunden. Vi bör även utvärdera möjligheten att använda mobila internetuppkopplingar under arbete på fältet för att minimera offline-scenarier helt.

Slutligen har kodbasen vuxit sig stor och komplex, och funktioner samt kodflöden måste dokumenteras för att undvika onödig tidsförlust vid framtida utveckling.

---

**Motivering:**  
Att kunna styra splatnedskalning direkt från UI:t gör det möjligt att snabbt nå en standard som fungerar bra för majoriteten av objekten, men också justera för unika krav. Detta förbättrar både flexibilitet och resultatkvalitet. Logging är kritisk för att kunna felsöka direkt vid fel i fotofasen, särskilt i ett scenario där arbetet sker mobilt och inte alltid är uppkopplat. Enbart lokal buffering räcker inte alltid – att även visa fel på ett tydligt sätt för operatören vid offlinearbete kan vara avgörande för att inte missa viktiga problem. Därför bör vi även överväga att använda mobil uppkoppling i riggarna där det är möjligt. Dokumentation är ett måste för att undvika framtida flaskhalsar – den ökade kodkomplexiteten gör att varje ny funktion eller justering annars kräver flera dagars ramp-up.

---

## Träning i molnet
- Horisontell skalning  
- Start/stop av compute efter behov  

**Beskrivning av arbetet:**  
Vi tränar för närvarande lokalt på två datorer med 3090-GPU:er, med möjlighet till en tredje som dock skulle innebära att vi tappar vår testmiljö och att Adam blir av med sina verktyg och skript. Dessa två datorer kan tillsammans träna cirka 30 dataset per dag. Med implementeringen av reducerad splatfilstorlek, som kräver att Nerfstudio körs flera gånger per objekt, sjunker kapaciteten troligtvis till 20–25 dataset per dag.  
För att undvika flaskhalsar vid stora kundvolymer eller parallella uppdrag behöver vi kunna skala träningen i molnet. På sikt vill vi ha möjlighet att starta en ny träningsinstans per dataset, så att träningen kan starta direkt efter att ett objekt är färdigfotat. För detta behöver vi bygga stöd för horisontell skalning, dynamisk start/stop av compute-resurser samt hantering av träningsjobb i parallell miljö.  

**Motivering:**  
Träning i molnet gör det möjligt att undvika flaskhalsar i produktionsflödet vid större kunduppdrag eller perioder med många samtidiga kunder. Initialt ger det oss flexibilitet och minimerar risken för förseningar. På längre sikt skapar det potentialen för att FOTO-3D-tjänsten kan erbjuda exempelvis leverans inom 24 timmar – en stark konkurrensfördel. Om AWS ger oss tillgång till flera GPU:er samtidigt, kan vi i teorin träna alla datasets parallellt och drastiskt korta ner leveranstiden för hela pipeline-processen.

---

## Skala viewer
- Skalning via ECS  

**Beskrivning av arbetet:**  
Vår viewer är idag uppsatt med AWS ECS Fargate och inkluderar funktioner som lastbalansering (ELB) och annan infrastruktur, men komponenten för faktisk automatisk skalning har ännu inte konfigurerats eller testats i skarpt läge. Inledande tester indikerar att vår nuvarande lösning klarar upp till cirka 1000 besökare per minut, men inga stresstester har gjorts där trafiktoppar sker samtidigt.  
Arbetet består i att sätta upp skalning i ECS, testa att köra minst tre instanser som grundlast och sedan stresstesta för att kartlägga var flaskhalsar uppstår. På längre sikt kan vi även utforska ytterligare AWS-funktionalitet som gör det möjligt att erbjuda "tre nior" i upptid (99.9 %) eller mer.

**Motivering:**  
Att kunna hantera oväntade trafiktoppar är avgörande om t.ex. en kund kör en kampanj eller en viral länk genererar mycket trafik. Kort sikt ger detta oss trygghet i att vi kan garantera grundläggande funktionalitet vid förväntad last. Långsiktigt ger det oss möjlighet att leverera en professionell tjänst med hög tillgänglighet, något som blir viktigare ju större våra kunder och användarbas blir.

---

## Bygga standardiserad pipeline
- Snabbare och mer enhetlig process  
- Undersöka automatisering  
- Möjlighet att ladda upp utanför AWS (mindre risk och enklare)  
- Namnstandard  
- Katalogisering av objekt för spårbarhet  
- Godkännandeprocess  

**Beskrivning av arbetet:**  
Vi har i nuläget inget effektivt sätt att spåra ett objekt genom hela vår pipeline vid skapandet av splats. Arbetet börjar med att dokumentera exakt hur vår process ser ut idag, från fotografering till färdig viewer, för att identifiera flaskhalsar eller steg som kan förbättras och/eller automatiseras. Ett centralt steg är att införa ett onboarding-flöde där varje objekt som ska konverteras till FOTO-3D registreras i Monday.com med namn och referensbild. Det namnet ska sedan följa med som standard genom hela flödet för att undvika förväxling av dataset, objekt och kunder.  
Vi ska också införa en tydlig **godkännandeprocess** i pipeline: t.ex. kontroll av kvalitet på träning, positionering och eventuell manuell justering innan objektet publiceras. På så sätt säkerställs att endast färdiga och godkända objekt går vidare till produktion.  
Om någon del i pipeline-flödet visar sig vara lämplig för automatisering (t.ex. generering av config, filhantering, filöverföring), ska vi väga tids- och utvecklingskostnad mot värdet det tillför.  
Som större teknikkomponent ska vi utvärdera och bygga ett verktyg eller API som automatiskt laddar upp färdiga splats till AWS S3, vilket löser både säkerhetsproblem och åtkomsthantering. Om den nya viewer-funktionalitet vi planerar att införa realiseras, kan vi även koppla detta steg till ett knapptryck — där en teammedlem efter pruning, alignering och godkännande klickar “Skicka till FOTO-3D-tjänsten”, vilket drastiskt effektiviserar flödet.

**Motivering:**  
En standardiserad pipeline minimerar risken för fel, förväxlingar och manuella missar, samtidigt som det skalar mycket bättre när fler personer blir involverade. Med rätt onboarding, namngivning och spårbarhet kan vi snabbt förstå vad som är gjort, vad som är kvar och vad som tillhör vem.  
En tydlig godkännandeprocess säkerställer kvalitet och minskar risken att halvfärdiga eller felaktiga modeller går till produktion.  
Automatisering och smidiga uppladdningar till S3 ger inte bara tekniska vinster utan även mycket tidsbesparing – framför allt efter träning. Jag bedömer att manuell efterbearbetning kan minskas med 50 % eller mer om processen kopplas ihop med en default-viewer-konfiguration och ett tydligt “skicka till produktion”-flöde.

---

## Vita riggen – lära av Robert
- Förstå projektet

**Beskrivning av arbetet:**  
Just nu är vita riggen det projekt jag har minst kunskap om. Arbetet innebär att jag sätter mig in i både hårdvara och mjukvara genom att gå igenom riggens funktioner tillsammans med Robert. Målet är att förstå riggens uppbyggnad, arbetsflöde och tekniska begränsningar eller styrkor, samt dokumentera detta. På sikt ska jag kunna felsöka och vid behov själv använda riggen i händelse av sjukdom eller frånvaro.

**Motivering:**  
Att ha kunskap om hur riggen fungerar skapar redundans i teamet, minskar beroendet av en person, och gör oss mindre sårbara vid tillfälliga bortfall. Det ger oss också möjlighet att vidareutveckla eller effektivisera riggen i framtiden, samt göra mer informerade beslut kring hårdvara, arbetsflöden eller automatisering inom FOTO-3D-processen.

---

## Wiki / Dokumentation
- Samla kunskap kring fotografering och objekt  
- Samlad plats för processer och lathundar  
- Lokal (mer jobb och underhåll) vs moln (mindre jobb men dyrare)  

**Beskrivning av arbetet:**  
Varje gång vi lär oss något nytt om hur man bäst fotograferar ett objekt, effektiviserar en process eller på annat sätt förbättrar vårt arbete, ska det dokumenteras i en intern wiki. Detta bör ske som en naturlig del av avslutsfasen för ett projekt. Exempelvis, om en kund har ett ovanligt objekt som krävde särskild ljussättning eller upphöjd placering, ska det skrivas ner och taggas med relevanta attribut (t.ex. objektform, material, kundnamn). På så sätt kan vi undvika att upprepa testning eller felsökning i framtiden.  
Wikin ska inte begränsas till fotografering, utan täcka alla processer och arbetsmoment som inte är direkt kopplade till kod (kodrelaterad dokumentation hålls separat i GitHub).  
Vi bör använda en lösning som **GitBook** eller liknande, vilket gör det möjligt att hantera både interna och kundriktade dokumentationer i samma system. Den stora fördelen med ett sådant system är att dokumentationen kan uppdateras löpande utan att påverka tillgängligheten på vår hemsida eller kräva omstarter. Det gör även arbetet med att bygga vår webbsida enklare, då kunddokumentation kan länkas in direkt istället för att behöva byggas in manuellt.
Denna metod är väldigt vanlig inom tech-företag. Ett exempel är fibbl.com, där dokumentationen finns på docs.fibbl.com – en separat webbplats som versionshanteras och uppdateras i takt med att tekniska aspekter i tjänsten förändras, utan att webbutvecklare behöver involveras.

**Motivering:**  
Att centralisera lärdomar och rutiner i en wiki sparar tid, minskar dubbelarbete och gör det enklare för nya teammedlemmar att komma in i arbetet. Istället för att varje person bygger upp kunskap själv, kan vi återanvända erfarenheter och lösningar från tidigare projekt. En välorganiserad wiki minskar också behovet av muntlig kunskapsöverföring och bidrar till ökad kvalitet, jämnare output och bättre skalbarhet av hela FOTO-3D-processen.  
Att använda ett verktyg som GitBook för detta ger oss en professionell, lättillgänglig och skalbar lösning för dokumentation — både internt och externt. Dessutom blir dokumentationsflödet frikopplat från vår webbplattform, vilket förenklar både underhåll och framtida utveckling.

---

## Kösystem
- Containerisering  
- Logging (vi tappar tid utan)  
- Servern opålitlig – överväg molnlösning eller ny hårdvara  
- Dokumentation  

**Beskrivning av arbetet:**  
Kösystemet är idag ett fristående Python-skript som körs direkt på en virtuell maskin på vår (ganska opålitliga) server. Alla typer av avbrott, som strömavbrott eller hårdvaruproblem, leder till ett totalstopp i träningspipeline. Dessa avbrott resulterar inte bara i ett stopp, utan även i att dataset helt enkelt inte tränas – utan att vi märker det förrän en eller två dagar senare, eftersom vi saknar realtidsloggning och notifieringar (som nämnts i uppgiften om loggingservern).  
Ett första steg är att containerisera kösystemet så att det kan återstartas automatiskt vid fel. Utöver detta behöver systemet få loggingfunktionalitet samt en redundant molnvariant som kan spinnas upp vid katastrofala fel, t.ex. hårdvarukrasch. Om en kund är aktiv och vår server går sönder står vi helt stilla tills en ny server är tillgänglig och konfigurerad, vilket även i bästa fall tar 4–5 timmar.  
Lösningen bör också inkludera ändringar i capture- och träningsskripten för att göra dem mer modulära, så att de kan kommunicera med flera potentiella kösystem (lokalt och i moln) med hjälp av en enkel heartbeat-funktion som verifierar tillgänglighet.

**Motivering:**  
Dagens kösystem är en svag punkt i vår infrastruktur – ett enda fel kan stoppa hela vår träningsproduktion. Avsaknaden av logging gör att vi ibland inte ens vet att ett dataset misslyckats förrän långt senare. Genom att containerisera och lägga till failover-lösningar i molnet ökar vi tillgängligheten markant. Det möjliggör också snabba återstarter och en stabil drift även om hårdvara havererar.  
Att kombinera detta med heartbeat-funktionalitet och fler mål för kommunikation i tränings- och capture-skripten innebär att vi kan känna oss trygga i att vår pipeline kan återställas på minuter, inte timmar – även om “servern brinner upp”.

---

## Intern katalog

**Beskrivning av arbetet:**  
Detta arbete innebär att vi skapar och konfigurerar en lösning för att få en överblick över alla FOTO-3D-modeller samt deras nuvarande status, såsom “I produktion”, “Demo”, “Test” osv.  
Idag finns ingen sammanhängande plats för att se alla aktiva länkar och vilken kund eller vilket objekt de tillhör. Monday.com är inte lämpat för att fungera som repository för live-länkar, så vi behöver hitta eller bygga ett alternativ.  
Tanken är att den person som ansvarar för det sista steget i modellskapandet manuellt lägger in länken och status i den valda lösningen. På sikt – när vi har ett CRM eller motsvarande – skulle denna process kunna automatiseras så att onboarding-personen tar hänsyn till CRM-information vid publicering.  
Vid ett mer avancerat framtida läge skulle modeller även kunna “stängas av” automatiskt, t.ex. vid avslutad prenumeration, antingen manuellt via CRM eller helt automatiserat.

**Motivering:**  
Utan ett centralt system för att hålla koll på aktiva modeller och deras tillstånd riskerar vi oordning, brutna länkar eller att kundkrav inte uppfylls. En intern katalog möjliggör snabb överblick, kvalitetssäkring, och bättre kundsupport.  
I det korta perspektivet skapar det tydlighet internt – i det långa perspektivet bygger det grunden för automation och integration med framtida CRM-system.

---

# Ej beslutat

## Adminpanel *(om vi går den vägen)*

**Beskrivning av arbetet:**  
Detta skulle bli ett betydligt större projekt jämfört med andra delar av vår pipeline och innefatta utveckling av frontend, backend, databaser, API:er, redundans, säkerhet, skalbarhet och mycket mer.  
Projektet skulle behöva brytas ner i etapper och specificeras ordentligt innan utveckling kan påbörjas.  
I vår kommande diskussion nästa vecka bör vi gå igenom en tydlig analys av kostnad/nytta och besluta om projektets omfattning. Om vi väljer att gå vidare bör scope hållas inom gränser som tillåter en kort "time to market".

**Motivering:**  
En adminpanel skulle ge våra kunder en central plats där de kan se och hantera sina 3D-visningar, vilket förbättrar upplevelsen och tillgängligheten av våra tjänster. Det öppnar även för framtida funktioner, som statistik, feedback, eller enklare konfigurationer. Samtidigt kan det effektivisera vår interna hantering. Men på grund av projektets komplexitet krävs noggrann planering och en tydlig avvägning mellan utvecklingstid och nytta.

---

## Marvify viewer-modul *(om vi går den vägen)*

**Beskrivning av arbetet:**  
Detta arbete skulle innebära att vi i praktiken outsourcar hostingen av viewer-modulen till kunden själv. Istället för att kunden bäddar in vår hostade viewer via en iframe, får de möjligheten att direkt importera viewer-komponenten i sin egen webbplats.  
Vi tar vår befintliga viewer-kodbas och anpassar den till en modul som kan importeras via CDN, med tydliga konfigurationsmöjligheter. Kunden skulle t.ex. kunna ställa in bakgrundsfärg, andra visuella parametrar och eventuella ytterligare inställningar vi väljer att exponera.  
Kunden måste själva sätta CORS-headers i sin webbserver för att det ska fungera, vilket vi instruerar i en medföljande dokumentation.  
Det enda vi fortsätter hosta är själva splats-filerna på vårt S3-konto. Viewer-delen ansvarar kunden själv för, vilket både minskar våra kostnader och gör lösningen mer flexibel för kunden.

**Motivering:**  
Detta ger våra kunder större kontroll över sin visningsupplevelse och en mer naturlig integration i deras webbsida utan begränsningar som kommer med iframes. Med enkla konfigurationsmöjligheter kan vi möta olika behov utan att varje kundintegration kräver specialkod.  
För oss innebär det att vi slipper underhålla frontend-hosting och därmed minskar vår infrastrukturkostnad samt teknisk support. Det minskar också behovet av att bygga denna typ av konfiguration i t.ex. en framtida adminpanel, eftersom kunden får direkt tillgång till anpassning via sin egen implementation.

---

## S3-tokenisering *(om vi går den vägen)*

**Beskrivning av arbetet:**  
Detta arbete hänger direkt ihop med viewer-modulen, då det krävs för att den ska fungera säkert. Vi behöver sätta upp ett API som accepterar tokens vi förser våra kunder med, och som genererar tidsbegränsade nedladdningslänkar till deras modeller i S3.  
Utöver det behöver vi bygga in skydd mot missbruk från både kunder och externa aktörer – exempelvis begränsningar i antal begäranden, IP-baserad spärr, loggning av åtkomst m.m.  
Kärnan i arbetet är att tillgängliggöra våra splats-filer i S3 endast för rättmätiga kunder, utan att exponera datan fritt eller obevakat.

**Motivering:**  
För att viewer-modulen ska fungera måste kunder kunna hämta sina modeller från vår S3-lagring. Samtidigt måste åtkomsten vara säkrad så att endast de kunder som har rätt får tillgång till sina specifika modeller.  
Tokenisering via ett API med tidsbegränsade länkar gör detta möjligt utan att kompromissa med säkerheten. Det ger oss kontroll, spårbarhet och flexibilitet – och öppnar även upp för framtida funktioner som statistik, åtkomstloggning och åtkomststyrning per kund.

---
