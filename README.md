# La Boîte de Fiches — Flashcards Français ⇄ Română

Aplicație de exersat vocabular francez-român, sub formă de PWA (Progressive Web App) instalabilă pe telefon. Aplicație soră a Karteikarten (Deutsch ⇄ Română), aceeași arhitectură și temă vizuală — „La Boîte de Fiches" e echivalentul firesc în franceză al conceptului „Karteikarten" (o cutie de fișe de cartotecă).

## Ce conține

- `index.html` — aplicația
- `vocab-data.js` — baza de vocabular (3541 cuvinte, niveluri A1-C2 complete, verificate manual, resortate după rangul real de frecvență)
- `manifest.json` — configurare PWA (nume, iconițe, mod de afișare)
- `sw.js` — service worker (funcționare offline)
- `icon-192.png`, `icon-512.png` — iconițele aplicației (aceeași temă vizuală și aceleași proporții ca Karteikarten DE-RO, cu banda adezivă tricoloră — albastru-alb-roșu, benzi verticale ca steagul francez — în loc de banda solidă a variantei germane, ca semn distinctiv de serie)

## Funcționalități

- Traducere franceză ⇄ română, grilă cu 4 variante de răspuns, cu distractori din aceeași categorie gramaticală (substantiv/verb/expresie/cuvânt funcțional)
- Niveluri selectabile A1–C2, combinabile între ele, plus **Cuvintele mele** (listă proprie), **Antonime & Sinonime** și **Conjugare verbe** — module noi, exclusiv franceze
- Sistem de priorități pe bază de streak (răspunsuri corecte consecutive) și stelute vizuale (aurii/verzi/roșii cu „iertare" după 3 reușite) — la A1-B2, cuvintele noi apar în ordinea reală de frecvență, pe benzi de 200
- **Cuvintele mele** — listă personală, cu adăugare din căutare (lipire din clipboard, evidențiată vizual, cu curățare automată a textului copiat din Reverso), suprascriere cu păstrarea progresului acumulat
- **Antonime & Sinonime** — 136 perechi antonime + 46 perechi sinonime, verificate manual, exclusiv în franceză
- **Conjugare verbe** — 100 dintre cele mai frecvente verbe franceze, la présent, imparfait, futur simple, passé composé și plus-que-parfait, cu reguli être/avoir corecte (inclusiv verbe reflexive) și acord de număr la participiu
- **🤖 AI (Claude)** — panou organizat ca hub, cu 3 destinații (opțional, experimental):
  - **Traducere & Corectură** — Traducere liberă (RO⇄FR, cu propria cheie API) într-un **pipeline în trei pași**: traducerea propriu-zisă, o revizuire separată (gramatică/ortografie/punctuație/topică, dar și fidelitate de sens, expresii idiomatice, cuvinte inventate), și — rar, doar când e nevoie — escaladarea bucăților incerte către un model mai avansat, pentru o a doua opinie; plus **Corectură franceză** (agent separat, dedicat identificării/corectării greșelilor dintr-un text scris de tine, cu explicații în română); ambele cu dictare vocală, imagine cu text (galerie/clipboard), export text/PDF
  - **📝 Exersează ce ai învățat** — text generat de Claude, STRICT din vocabularul deja exersat cu succes (prag: minim 2 răspunsuri corecte per cuvânt), pe o temă la alegere, cu traducere ascunsă până o ceri și loc pentru propria încercare înainte
  - **🆕 Cuvinte noi în context** — 3 texte scurte independente, generate din cuvinte abia întâlnite (văzute 1-2 ori), cu traducere vizibilă direct și cuvintele țintă evidențiate cu roșu, la orice formă gramaticală naturală; selecție automată (gratuită, din progres) sau manuală (din lista „Cuvintele mele exersate", accesibilă și din Setări)
  - **📜 Istoric** — toate traducerile/corecturile/exercițiile AI, cu filtrare, selecție/ștergere în masă, export JSON/CSV/PDF, import cu deduplicare, și analiză de cuvinte frecvente neadăugate încă în vocabular
- Selector de direcție: FR→RO, RO→FR, sau ambele amestecat
- Pronunție audio a cuvintelor franceze (Web Speech API), cu alegere de voce
- Link direct către Reverso (`dictionary.reverso.net/french-romanian`) pentru fiecare cuvânt francez, ca sursă suplimentară (dict.cc nu are pereche franceză-română directă)
- Buton "Sari peste" pentru a trece la următorul cuvânt fără să conteze ca greșeală
- Căutare vocală (cu recunoaștere a elidării franceze: „l'ami" → „ami")
- Încărcare de liste proprii de vocabular (CSV, TSV sau XLSX)
- Export al listei curente, statisticilor, și „Cuvintelor mele", ca fișiere CSV
- Backup complet (progres + preferințe) exportabil/importabil ca fișier .json
- Preferințele (niveluri, direcție, mod) și statisticile se salvează local, în browser, per dispozitiv

## Instalare pe telefon

1. Deschide link-ul GitHub Pages al acestui repository, în Chrome (Android) sau Safari (iOS)
2. Din meniul browserului, alege "Adaugă la ecranul principal" / "Instalează aplicația"
3. Aplicația apare cu propria iconiță și funcționează parțial offline

## Actualizarea aplicației

Pentru a publica o versiune nouă: încarcă fișierele modificate în acest repository (Add file → Upload files → Commit), GitHub Pages redeploy-ează automat în 1-2 minute. Aplicația instalată pe telefon preia schimbările la următoarea deschidere.

## Changelog

**v28** — 4 corecții la modulul „Cuvinte noi în context" (nou în v27), găsite la testare reală:
1. **Listă fără scroll propriu** — „Cuvintele mele exersate" afișa toate cuvintele ca un perete de etichete, fără zonă limitată; acum are propria zonă scrolabilă (max 38% din înălțimea ecranului), independentă de restul panoului.
2. **Cuvinte invariabile confundate cu cuvinte diferite ce încep la fel** — cuvântul țintă „par" (prepoziție) genera/marca greșit „parler", „partir", „parce que" în loc să folosească „par" însuși — modelul interpreta „adaptează la orice formă gramaticală" ca „găsește un cuvânt înrudit care poate fi conjugat", chiar și pentru cuvinte invariabile care n-au deloc forme flexionate. Reparat în **ambele** prompturi (generare + marcare), cu distincție explicită variabil/invariabil și exemplul exact raportat, ca exemplu concret negativ.
3. **Filtrul de nivel din listă nu acoperea C1/C2 deloc** — avea doar gruparea grosieră A1-A2/B1-B2; extins la toate cele 6 niveluri CEFR individuale, plus „Cuvintele mele" separat. Reparată și o legătură ruptă rezultată din asta (generarea manuală deducea acum corect nivelul din cuvintele alese, nu din vechiul filtru pe grupuri).
4. **Sortare după nivel, lipsă** — exista doar stelute/alfabetic; adăugată, cu ordinea CEFR corectă (A1→C2).
5. **Bonus, neraportat dar găsit pe drum**: butonul de confirmare a selecției nu era vizibil constant la liste lungi — acum „flotant" (`position:sticky`), rămâne la baza zonei vizibile indiferent cât ai scrollat prin cuvinte.

Toate testate programatic (16 verificări suplimentare) și verificate cu regresie pe bug-urile critice anterioare (selecția multiplă de niveluri, v24) — 0 erori.

**v27** — modul nou, mare: **🆕 Cuvinte noi în context**. Diferit de „Exersează ce ai învățat" — aici nu te testezi, ci vezi cuvinte abia întâlnite (văzute o dată sau de două ori) folosite natural, de mai multe ori, în situații diferite, cu traducerea română vizibilă direct (nu ascunsă).
- **Selecție cuvinte** — automată, direct din progres (fără AI, gratuit, instant), sau manuală, dintr-o listă nouă și separată, „📋 Cuvintele mele exersate" (accesibilă și din ⚙ Setări pentru răsfoit liber, cu filtre de nivel și sortare), plafon 5 cuvinte.
- **Pipeline în 3 agenți**: (1) generare — 3 texte scurte, independente, fiecare folosind TOATE cuvintele țintă cel puțin o dată, la orice formă gramaticală naturală cere contextul; (2) revizuire — reutilizează agentul de gramatică/ortografie + escaladarea existente, aplicat pe liniile extrase din toate cele 3 texte, recombinate apoi pe baza numărului de linii reținut înainte de revizuire; (3) marcare — un agent nou, dedicat, încadrează cu `{{...}}` fiecare apariție a cuvintelor țintă în liniile franceze finale, cu **verificare de siguranță pe linie** (dacă eliminarea marcajelor nu reproduce exact linia originală, acea linie rămâne simplă, fără evidențiere).
- **Randare marker-aware, centralizată** — `parseTaggedAiResult()` transformă acum `{{cuvânt}}` în evidențiere roșie oriunde apare, deci Istoricul și exportul beneficiază automat, fără cod duplicat; citirea cu voce și exportul text/PDF curăță marcajele automat.
- **Plasă de siguranță pentru format lipsă** — dacă `[TEXT1]`/`[TEXT2]`/`[TEXT3]` lipsesc complet din răspuns, conținutul `[FR]`/`[RO]` existent e recuperat și împărțit în 3, în loc de casete goale.
- Istoric — sursă nouă, `[nou]`, cu evidențierea păstrată la redeschidere (se salvează textul final, marcat și revizuit, nu ciorna dinaintea marcării).
- **Testat programatic, exhaustiv**: 26 de verificări (5 obligatorii + bonus) — extragere/recombinare cu revizuire simulată, `splitIntoThreeTexts` pe format normal ȘI complet absent, `extractCoreWord` pe cazul real din vocabular, `deriveLevelGroupFromWords` pe toate cazurile (majoritate/egalitate/fără nivel clar), confirmare că promptul conține explicit nivelul țintă, randare marker-aware, și plasa de siguranță pe linie — toate trecute.
- **Bug real găsit pe drum**: `mistakeIds` e `Array`, nu `Set` — codul nou folosea `.has()`, care ar fi aruncat eroare la filtrul „doar cu greșeală activă"; corectat la `.includes()`.
- Regresie verificată: selecția multiplă de niveluri (A1+Conjugare verbe+C1+C2+Antonime, bug reparat la v24) — 50 de runde, 0 erori.

**v26** — bug vizual reparat: chip-ul de direcție de pe carduri (deasupra întrebării) afișa „DE → RO"/„RO → DE" în loc de „FR → RO"/„RO → FR" — text rămas hardcodat dintr-o versiune veche, într-un loc pe care scanările automate de „reziduuri germane" nu-l prinseseră (nu conținea cuvinte căutate ca „german"/„Karteikarten", doar litera „DE" izolată). Restul logicii (ce parte a cardului arată franceza vs. română) era deja corectă — doar eticheta afișată era greșită. Verificat funcțional pe toate cele 3 opțiuni de direcție (FR→RO, RO→FR, mixt).

**v25** — pipeline de traducere extins de la 2 la 3 pași, plus 4 categorii noi de verificare la revizuire.
- **Promptul de revizuire (pasul 2)** acoperea deja topică și acord gen/număr articol-substantiv, dar îi lipseau: **acordul participiilor** (cu „a fi"/pasiv, separat de acordul articol-substantiv), **fidelitate de sens** (o propoziție poate fi corectă gramatical dar să spună altceva decât originalul), **expresii idiomatice** (traduse mecanic, cuvânt-cu-cuvânt, în loc de echivalentul natural din limba țintă), și **interzicerea cuvintelor inventate** (compuse fabricate, plauzibile dar inexistente). Toate patru adăugate, fiecare cu exemplu concret negativ+pozitiv (regulile abstracte nu sunt suficiente pentru un model mic — aceeași lecție aplicată deja la cratime/acord).
- **Pas nou, al treilea, rar și țintit**: dacă la revizuire modelul întâlnește o bucată de care chiar nu e sigur (nu ezitare minoră de stil), o marchează explicit (`[UNCERTAIN]...[/UNCERTAIN]`) în loc să ghicească — doar acea bucată exactă (nu tot textul) e trimisă mai departe către un model mai capabil (`claude-sonnet-5`), pentru o a doua opinie. Cost suplimentar doar când chiar e nevoie, nu la fiecare traducere.
- **`callClaude`** primește acum parametru opțional de model (implicit tot Haiku pentru restul aplicației — neschimbat).
- **Testat programatic, exhaustiv**: extragere segmente marcate (fără marcaje / un marcaj / mai multe, cu ordinea păstrată), recombinare corectă după „rezolvare", fallback sigur la nepotrivire de număr de răspunsuri sau la eroare de rețea, și confirmare că mecanismul NU se declanșează deloc (fără apel API suplimentar) când nu există nimic marcat — 15 verificări, toate trecute.

**v24** — bug critic reparat: pagină aproape goală / rundă nouă blocată la selecții multiple de niveluri.
- **Cauza exactă**: la construirea unei runde, pentru fiecare cuvânt normal (A1-C2) se calculau distractori parcurgând TOATE cuvintele active — dar dacă erau selectate simultan și nivelurile „Conjugare verbe" și/sau „Antonime & Sinonime" (structuri de date complet diferite, fără câmpul `.fr`), funcția de clasificare gramaticală (`classifyWord`) crăpa pe ele (`Cannot read properties of undefined (reading 'trim')`), oprind tăcut toată construcția rundei.
- **De-aici veneau exact simptomele descrise**: pagină goală (eroare neafișată, doar conținut vechi rămas), intermitent (depindea de ce combinație de cuvinte extrăgea aleatoriu eșantionul rundei — uneori pica pe combinația care crăpa, uneori nu, explicând de ce „după câteva refresh-uri apar"), și butonul „Rundă nouă" blocat (apela aceeași funcție afectată).
- **Fix**: distractorii unui cuvânt normal se aleg acum strict din alte cuvinte normale, excluzând explicit intrările „Conjugare verbe"/„Antonime & Sinonime" din calcul (oricum n-ar fi avut sens ca distractori pentru o întrebare de traducere obișnuită).
- **Verificat riguros**: reprodus bug-ul cu certitudine (eroare exactă confirmată pe codul vechi), apoi testat fix-ul pe 13 combinații diferite de niveluri × 30 de runde fiecare (390 runde total, inclusiv toate nivelurile + Verbe + Antonime simultan) — 0 erori.

**v23** — corecție de calitate a traducerii, găsită prin testare pe text real (articol Le Monde): „une aide" era tradus greșit „o ajutoare" (formă de plural, articulată greșit la singular — corect: „un ajutor"). Nu era doar o greșeală izolată, ci un gol real în pipeline-ul de doi agenți:
1. **Promptul de traducere** (agentul 1) — adăugată o regulă explicită despre acordul gen/număr al substantivelor românești alese, cu exemplul concret „o ajutoare"→„un ajutor" (regulile abstracte nu sunt suficiente pentru un model mic ca Haiku — are nevoie de exemplu concret, negativ+pozitiv, aceeași lecție aplicată deja la cratime).
2. **Promptul de revizuire gramaticală** (agentul 2) — menționa doar acorduri adjectiv-substantiv/participiu-subiect, dar **omitea explicit acordul articol-substantiv** (exact cazul „o ajutoare"); plus, formularea „NU înlocuiești cuvinte" risca să fie interpretată prea larg, tratând o formă greșită ca pe o alegere deliberată de netins. Clarificat explicit: corectarea formei (gen/număr) unui cuvânt deja ales nu e „înlocuire de cuvânt".
3. **Plasă de siguranță întărită** — verificarea că rezultatul revizuit e valid controla doar dacă mai are etichete `[FR]/[RO]`, nu și dacă numărul de perechi s-a păstrat; la texte lungi, multi-paragraf, o pierdere/contopire silențioasă de conținut la pasul 2 ar fi trecut neobservată. Acum se compară explicit numărul de perechi înainte/după revizuire — dacă nu se potrivește, se păstrează traducerea nerevizuită (mai sigură decât una scurtată).
4. Notă onestă adăugată în textul de ajutor despre limitele reale ale modelului Haiku (cel mai ieftin) pe texte lungi/complexe.

**v22** — 3 timpuri noi la modulul „Conjugare verbe": imparfait, plus-que-parfait, futur simple (pe lângă présent și passé composé, existente deja). Lista de verbe redusă de la 136 la **100, cele mai frecvente** (după rangul real din `fr_50k.txt`), ca extinderea la 5 timpuri să nu se piardă în cazuri rare.
- **Imparfait** — derivat algoritmic (rădăcina de la „nous" prezent minus „-ons"), cu excepția reală unică din toată limba (être) și 3 excepții tehnice de ortografie (manger/changer/commencer, unde nous/vous pierd „e"/„ç"-ul suplimentar).
- **Futur simple** — regulă generală (infinitiv, cu -re care pierde „e" final) + tabel de rădăcini neregulate pentru ~15 verbe frecvente (être→ser-, aller→ir-, faire→fer-, venir→viendr- etc.), inclusiv dublarea de consoană la appeler (appellerai) și mourir (mourrai).
- **Plus-que-parfait** — auxiliarul la imperfect + același participiu/acord de la passé composé, fără date noi, doar reutilizare de cod.
- **Bug real găsit la testare**: elidarea reflexivă (m'/t'/s' vs. me/te/se) era calculată static, presupunând doar formele de prezent ale lui être (unde doar „es"/„est" încep cu vocală) — la plus-que-parfait, auxiliarul e la imperfect, unde TOATE cele 6 forme (étais/était/étions...) încep cu vocală, deci toate persoanele reflexive au nevoie de elidare, nu doar 2. Corectat: elidarea se calculează acum dinamic, după prima literă a formei reale de auxiliar folosite, nu dintr-un tabel fix.
- **Testat exhaustiv**: toate cele 3000 de întrebări posibile (100 verbe × 6 persoane × 5 timpuri) au exact 4 opțiuni unice; verificare suplimentară, automată, că nu mai există nicio formă reflexivă neelidată greșit, nicăieri.

**v21** — verificare de audit după v20 (fără funcționalitate nouă, doar corecții de precizie):
1. **0 reziduuri germane găsite** — scanare exhaustivă (text, cod, ID-uri HTML, clase CSS, funcții) — nimic rămas din Karteikarten.
2. **Paritate completă cu germana confirmată programatic** — comparație funcție-cu-funcție, ID-cu-ID, clasă-cu-clasă între cele două `index.html`; singurele diferențe sunt cele franceze specifice, așteptate (Corectură franceză, elidare, passé composé etc.) — nimic lipsă (în afara modulului „Îngrijire"/PFLEGE, exclus intenționat, nefiind relevant pentru franceză).
3. **Corecții text de Ajutor** — descrierea modulului AI încă spunea „două funcții separate", frazare rămasă de dinainte de restructurarea în hub (v20); actualizată să reflecte cele 3 destinații. O altă frază („redirecționează spre exercițiu") era ambiguă după apariția modulului nou „Exersează ce ai învățat" cu acest nume exact — clarificată.
4. Secțiunea de Confidențialitate menționează acum explicit istoricul AI ca dată stocată local.
5. **15 teste funcționale suplimentare** (DOM real, jsdom) — navigare hub completă, prag „cunoscut", salvare/randare istoric cu tag-uri corecte, verificare de regresie pe Verbe/Antonime — toate trecute.

**v20** — replicat din Karteikarten (aplicația-soră germană): două module noi mari, plus restructurare a panoului AI.
- **🤖 Panoul AI restructurat ca hub** — 3 destinații: Traducere & Corectură (ce exista deja), 📝 Exersează ce ai învățat (nou), 📜 Istoric (nou).
- **📝 Exersează ce ai învățat** — Claude generează un text scurt, pe o temă la alegere, folosind STRICT vocabularul deja exersat cu succes (prag exact: cel puțin 2 răspunsuri corecte, cumulat, per cuvânt) — nu tot vocabularul din aplicație. Grupare pe 2 niveluri (A1-A2 → max 60 cuvinte; B1-B2 → max 100, cu A1-A2 permis liber ca bază gramaticală). Plafon strict de 15% cuvinte din afara listei cunoscute. Direcție aleasă manual (FR sau RO). Traducerea rămâne ascunsă până apeși „Arată traducerea", cu loc pentru propria încercare înainte — comparație directă, salvată automat în Istoric.
- **📜 Istoric** — toate traducerile/corecturile/exercițiile AI, cu filtrare an/lună, sortare, selecție și ștergere în masă, view de detaliu (inclusiv „Exersarea ta" vs. traducerea corectă, la exerciții), export JSON (pentru combinat între dispozitive)/CSV/PDF, import cu deduplicare automată, și analiză de „cuvinte frecvente, neadăugate" (scanează istoricul, sugerează cuvinte franceze repetate de 2+ ori, absente din vocabular — adăugare cu un tap).
- **Bug real găsit pe drum**: fișierul avea două implementări duplicate ale pipeline-ului de revizuire gramaticală (de la o versiune anterioară), care rulau de două ori la fiecare traducere — consolidat la o singură trecere.

**v19** — corecție de gramatică română: eticheta implicită de pe cardurile modului obișnuit de traducere era „Traduce" (fără sens gramatical clar ca instrucțiune) — corectată la „Tradu" (imperativ informal singular), consecvent cu tonul „tu" folosit peste tot în restul aplicației (texte de ajutor, mesaje). Etichetele proprii de la Antonime/Sinonime/Conjugare rămân neschimbate.

**v18** — completare la fix-ul de la v17 (separarea `localStorage`): restaurarea unui backup **vechi** (exportat înainte de prefixare) nu mai afișează fals „Backup restaurat" fără să restaureze de fapt nimic (fiindcă niciuna dintre cheile vechi nu se mai potrivea cu `BACKUP_KEYS`, actualizat la cele prefixate) — acum verifică explicit dacă există cel puțin o cheie compatibilă în fișier înainte de a cere confirmare; dacă nu găsește niciuna, oprește procesul cu un mesaj clar, fără să reîncarce aplicația.

**v17** — trei corecții găsite în timp ce lucram la aplicația soră de greacă (arhitectură identică):
1. **Amestec de date între aplicații** — toate cele 9 chei `localStorage` folosite (`wordStats`, `prefs`, `mistakeIds`, `myWords`, `voiceURI`, `installBannerDismissed`, `streak`, `fontZoom`, `claudeApiKey`) au fost prefixate cu `boitedefiches_`, inclusiv în `BACKUP_KEYS` — altfel, fiindcă toate aplicațiile-soră (germană, franceză, greacă) sunt găzduite pe același domeniu GitHub Pages, `localStorage` fiind izolat per domeniu (nu per aplicație), își suprascriau reciproc progresul. Notă: progresul salvat anterior rămâne sub cheile vechi, necitit după acest update — aplicația pornește curat.
2. **Zoom-ul de bază (A−/A+) rămâne mereu vizibil** pe ecrane înguste — doar procentul și butonul de resetare se ascund sub ~420px lățime.
3. **Layout topbar mobil** — numele aplicației se trunchiază cu „..." dacă nu încape, în loc să împingă butonul de Setări pe un rând nou; grupul din dreapta (căutare vocală/AI/setări) rămâne compact, pe același rând.

## Surse și atribuiri

- **Selecția și nivelizarea cuvintelor** sunt construite **integral și independent** din rangul de frecvență reală de utilizare a limbii franceze, pe baza listei [hermitdave/FrequencyWords](https://github.com/hermitdave/FrequencyWords) (`content/2018/fr/fr_50k.txt`, derivată din corpus OpenSubtitles), licență **MIT**. Cuvintele sunt lematizate (formă de bază + tip gramatical) cu spaCy (`fr_core_news_sm`), verificate manual pentru a elimina nume proprii, forme flexionate duplicate și zgomot din subtitrări, apoi împărțite pe niveluri A1–C2 după poziția lor în clasamentul de frecvență. Nicio parte din selecție nu depinde de curriculumul vreunei instituții de examinare.
- Etichetele CEFR (A1, A2, B1, B2, C1, C2) sunt un standard public, deschis, al Consiliului Europei — nu proprietatea vreunei organizații.
- Toate cele 6 niveluri sunt complete: A1 (519), A2 (477), B1 (763), B2 (538), C1 (342), C2 (902) — **3541 de cuvinte în total**. La rang mare (C1/C2), frecvența e un indiciu mai slab pentru dificultate reală, iar corpusul conține un procent mult mai mare de nume proprii/personaje din subtitrări (sute excluse manual) și cuvinte vulgare. Ordinea din interiorul fiecărui nivel reflectă rangul real de frecvență (esențial pentru sistemul de benzi/priorități) — verificată și resortată integral.
- **Corecție manuală suplimentară de nivel**: cuvinte foarte banale (numerele de bază 1-90, culori de bază, animale/mâncare/corp comune) au fost mutate la nivelul CEFR corespunzător chiar și acolo unde frecvența lor brută în corpus le-ar fi plasat mai sus — subtitrările nu numără sau colorează la fel de des cum vorbesc despre alte teme. Exemplu concret: numerele de bază (`un`, `deux`, `trois`...) lipseau aproape complet din selecția inițială, pentru că extragerea automată exclude categoria gramaticală „numeral" alături de cifre/simboluri — corectat manual.
- Traducerile în limba română sunt muncă originală.
- Acest proiect e o resursă personală de studiu, nu revendică nicio afiliere cu hermitdave, Reverso, Anthropic sau alte instituții/persoane menționate.

## Confidențialitate

Aplicația nu colectează, nu transmite și nu stochează nicio dată pe niciun server propriu. Tot ce ține de progres (statistici, preferințe, „Cuvintele mele", istoricul AI) rămâne local, în browser-ul dispozitivului tău. Conexiuni externe: Google Fonts (fonturi), Reverso (doar dacă apeși linkul respectiv), motorul de sinteză vocală al telefonului, motorul de recunoaștere vocală al browserului (dacă folosești căutarea/dictarea vocală — trimite sunetul către serverele browserului, ex. Google pentru Chrome, ca să fie transformat în text), și — doar dacă activezi opțional funcția AI (Claude) și adaugi propria cheie API — serverele Anthropic, pentru traducerile/corecturile/exercițiile cerute explicit. Cheia API rămâne salvată doar local, nu trece niciodată prin noi.

## Licență

Codul aplicației (`index.html`, `sw.js`, `manifest.json`) e disponibil liber pentru refolosire și modificare personală. Vocabularul urmează atribuirile de mai sus (MIT pentru selecția de frecvență; traducerile românești sunt libere de folosit, fără garanții).

## Disclaimer

Vocabularul și traducerile pot conține ocazional imprecizii; verifică independent (ex. Reverso, linkul din aplicație) orice cuvânt de care nu ești sigur. Aplicația nu oferă consultanță de niciun fel — e strict un instrument de exersare, oferit "ca atare", fără nicio garanție.

## Donații / susținere

Aplicația **nu are** (deocamdată) niciun buton de donații (Ko-fi, Buy Me a Coffee etc.) și nu e monetizată în niciun fel. E un proiect personal, făcut pentru uz propriu și distribuit liber.
