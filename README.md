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
- **Conjugare verbe** — 136 verbe, présent + passé composé, cu reguli être/avoir corecte (inclusiv verbe reflexive) și acord de număr la participiu
- **🤖 AI (Claude)** — două funcții comutabile dintr-un toggle: **Traducere** liberă (RO⇄FR, cu propria cheie API), acum într-un **pipeline în doi pași** — un agent alege traducerea optimă, apoi un al doilea, specializat strict pe gramatică/ortografie/punctuație/topică, o revizuiește tehnic înainte de afișare (fără să schimbe alegerea de traducere) — și **Corectură franceză** (agent separat, dedicat exclusiv identificării și corectării greșelilor dintr-un text scris de tine, cu explicații în română pentru fiecare greșeală găsită); ambele cu dictare vocală, imagine cu text (galerie/clipboard), export text/PDF — opțional, experimental
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

Aplicația nu colectează, nu transmite și nu stochează nicio dată pe niciun server propriu. Tot ce ține de progres (statistici, preferințe, „Cuvintele mele") rămâne local, în browser-ul dispozitivului tău. Conexiuni externe: Google Fonts (fonturi), Reverso (doar dacă apeși linkul respectiv), motorul de sinteză vocală al telefonului, motorul de recunoaștere vocală al browserului (dacă folosești căutarea/dictarea vocală — trimite sunetul către serverele browserului, ex. Google pentru Chrome, ca să fie transformat în text), și — doar dacă activezi opțional funcția AI (Claude) și adaugi propria cheie API — serverele Anthropic, pentru traducerile cerute explicit. Cheia API rămâne salvată doar local, nu trece niciodată prin noi.

## Licență

Codul aplicației (`index.html`, `sw.js`, `manifest.json`) e disponibil liber pentru refolosire și modificare personală. Vocabularul urmează atribuirile de mai sus (MIT pentru selecția de frecvență; traducerile românești sunt libere de folosit, fără garanții).

## Disclaimer

Vocabularul și traducerile pot conține ocazional imprecizii; verifică independent (ex. Reverso, linkul din aplicație) orice cuvânt de care nu ești sigur. Aplicația nu oferă consultanță de niciun fel — e strict un instrument de exersare, oferit "ca atare", fără nicio garanție.

## Donații / susținere

Aplicația **nu are** (deocamdată) niciun buton de donații (Ko-fi, Buy Me a Coffee etc.) și nu e monetizată în niciun fel. E un proiect personal, făcut pentru uz propriu și distribuit liber.
