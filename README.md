# La Boîte de Fiches — Flashcards Français ⇄ Română

Aplicație de exersat vocabular francez-român, sub formă de PWA (Progressive Web App) instalabilă pe telefon. Aplicație soră a Karteikarten (Deutsch ⇄ Română), aceeași arhitectură și temă vizuală — „La Boîte de Fiches" e echivalentul firesc în franceză al conceptului „Karteikarten" (o cutie de fișe de cartotecă).

## Ce conține

- `index.html` — aplicația
- `vocab-data.js` — baza de vocabular (3543 cuvinte, niveluri A1-C2 complete, verificate manual)
- `manifest.json` — configurare PWA (nume, iconițe, mod de afișare)
- `sw.js` — service worker (funcționare offline)
- `icon-192.png`, `icon-512.png` — iconițele aplicației (aceeași temă vizuală ca Karteikarten DE-RO, cu bandă adezivă albastru-petrol în loc de auriu, ca semn distinctiv de serie)

## Funcționalități

- Traducere franceză ⇄ română, grilă cu 4 variante de răspuns, cu distractori din aceeași categorie gramaticală (substantiv/verb/expresie/cuvânt funcțional)
- Niveluri selectabile A1–C2, combinabile între ele
- Selector de direcție: FR→RO, RO→FR, sau ambele amestecat
- Mod de exersare "inteligent" (repetiție spațiată bazată pe istoricul de răspunsuri) sau complet aleator
- Pronunție audio a cuvintelor franceze (Web Speech API), cu alegere de voce
- Link direct către Reverso (`dictionary.reverso.net/french-romanian`) pentru fiecare cuvânt francez, ca sursă suplimentară (dict.cc nu are pereche franceză-română directă)
- Buton "Sari peste" pentru a trece la următorul cuvânt fără să conteze ca greșeală
- Încărcare de liste proprii de vocabular (CSV, TSV sau XLSX)
- Export al listei curente și al statisticilor, ca fișiere CSV
- Preferințele (niveluri, direcție, mod) și statisticile se salvează local, în browser, per dispozitiv

## Instalare pe telefon

1. Deschide link-ul GitHub Pages al acestui repository, în Chrome (Android) sau Safari (iOS)
2. Din meniul browserului, alege "Adaugă la ecranul principal" / "Instalează aplicația"
3. Aplicația apare cu propria iconiță și funcționează parțial offline

## Actualizarea aplicației

Pentru a publica o versiune nouă: încarcă fișierele modificate în acest repository (Add file → Upload files → Commit), GitHub Pages redeploy-ează automat în 1-2 minute. Aplicația instalată pe telefon preia schimbările la următoarea deschidere.

## Surse și atribuiri

- **Selecția și nivelizarea cuvintelor** sunt construite **integral și independent** din rangul de frecvență reală de utilizare a limbii franceze, pe baza listei [hermitdave/FrequencyWords](https://github.com/hermitdave/FrequencyWords) (`content/2018/fr/fr_50k.txt`, derivată din corpus OpenSubtitles), licență **MIT**. Cuvintele sunt lematizate (formă de bază + tip gramatical) cu spaCy (`fr_core_news_sm`), verificate manual pentru a elimina nume proprii, forme flexionate duplicate și zgomot din subtitrări, apoi împărțite pe niveluri A1–C2 după poziția lor în clasamentul de frecvență. Nicio parte din selecție nu depinde de curriculumul vreunei instituții de examinare.
- Etichetele CEFR (A1, A2, B1, B2, C1, C2) sunt un standard public, deschis, al Consiliului Europei — nu proprietatea vreunei organizații.
- Toate cele 6 niveluri sunt complete: A1 (519), A2 (477), B1 (763), B2 (538), C1 (342), C2 (904) — **3543 de cuvinte în total**. La rang mare (C1/C2), frecvența e un indiciu mai slab pentru dificultate reală, iar corpusul conține un procent mult mai mare de nume proprii/personaje din subtitrări (sute excluse manual) și cuvinte vulgare.
- **Corecție manuală suplimentară de nivel**: cuvinte foarte banale (numerele de bază 1-90, culori de bază, animale/mâncare/corp comune) au fost mutate la nivelul CEFR corespunzător chiar și acolo unde frecvența lor brută în corpus le-ar fi plasat mai sus — subtitrările nu numără sau colorează la fel de des cum vorbesc despre alte teme. Exemplu concret: numerele de bază (`un`, `deux`, `trois`...) lipseau aproape complet din selecția inițială, pentru că extragerea automată exclude categoria gramaticală „numeral" alături de cifre/simboluri — corectat manual.
- Traducerile în limba română sunt muncă originală.
- Acest proiect e o resursă personală de studiu, nu revendică nicio afiliere cu hermitdave, Reverso, Anthropic sau alte instituții/persoane menționate.

## Confidențialitate

Aplicația nu colectează, nu transmite și nu stochează nicio dată pe niciun server. Tot ce ține de progres (statistici, preferințe) rămâne local, în browser-ul dispozitivului tău. Singurele conexiuni externe sunt: Google Fonts (fonturi), Reverso (doar dacă apeși linkul respectiv) și motorul de sinteză vocală al telefonului.

## Licență

Codul aplicației (`index.html`, `sw.js`, `manifest.json`) e disponibil liber pentru refolosire și modificare personală. Vocabularul urmează atribuirile de mai sus (MIT pentru selecția de frecvență; traducerile românești sunt libere de folosit, fără garanții).

## Disclaimer

Vocabularul și traducerile pot conține ocazional imprecizii; verifică independent (ex. Reverso, linkul din aplicație) orice cuvânt de care nu ești sigur. Aplicația nu oferă consultanță de niciun fel — e strict un instrument de exersare, oferit "ca atare", fără nicio garanție.

## Donații / susținere

Aplicația **nu are** (deocamdată) niciun buton de donații (Ko-fi, Buy Me a Coffee etc.) și nu e monetizată în niciun fel. E un proiect personal, făcut pentru uz propriu și distribuit liber.
