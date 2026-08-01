# Diagnoza: „korepetycje język polski" — brak widoczności polskimatura.pl

Data analizy: 2026-08-01
Fraza docelowa: **korepetycje język polski**
Objaw zgłoszony: brak witryny w wynikach do 22. strony Google (≈ poza pozycją 220).

---

## 1. Co udało się ustalić (i czym to potwierdzone)

Analiza była prowadzona wyłącznie na podstawie tego, co widzi wyszukiwarka
(zapytania `site:`, zapytania brandowe i frazowe). Sieć wychodząca w tym środowisku
jest zablokowana przez politykę sandboksa, więc **nie udało się pobrać źródła HTML
polskimatura.pl ani pliku robots.txt** — punkty oznaczone „do weryfikacji" wymagają
sprawdzenia w Search Console. Wnioski główne nie zależą jednak od tej weryfikacji,
bo opierają się na samym indeksie Google.

| Ustalenie | Dowód |
|---|---|
| Witryna **jest zaindeksowana**, i to szeroko | `site:polskimatura.pl` zwraca strona główna, `/epoki/...`, `/autorzy-teksty/...`, `/test/...`, `/polonista/...`, `/motyw-winy-i-kary.html` |
| **Nie istnieje strona docelowa dla frazy** | `site:polskimatura.pl korepetycje` **nie zwraca żadnej podstrony o korepetycjach** — zwraca strony o lekturach i epokach |
| Słowo „korepetycje" występuje jako **boilerplate** | te same krótkie formułki o lekcjach online + telefon 512 858 679 pojawiają się w snippetach stron o Baczyńskim, Morsztynie, Lilli Wenedzie itd. |
| Title witryny celuje w **inną intencję** | title strony głównej: „Matura z polskiego – lektury, epoki i testy \| polskimatura.pl" — brak słowa „korepetycje" |
| SERP należy do **agregatorów** | TOP frazy: OLX, e-korepetycje.net, korepetycje.pl, superprof.pl, preply.com, e-korepetytor.com.pl, bukischool.com.pl, educat.study |

**To nie jest problem techniczny.** Skoro Google trzyma w indeksie setki podstron
serwisu, to nie ma tu ani blokady w `robots.txt`, ani `noindex`, ani kary,
ani problemu z renderowaniem. Gdyby przyczyną było indeksowanie, zniknęłyby
wszystkie frazy, a nie jedna.

---

## 2. Przyczyna

### Przyczyna główna — brak strony docelowej

**Google pozycjonuje strony, nie witryny.** Żeby serwis mógł wystąpić na frazę
„korepetycje język polski", musi istnieć URL, którego *tematem* jest ta usługa.
Takiego URL-a nie ma. Nie ma `/korepetycje/`, nie ma `/korepetycje-jezyk-polski/`
— nic. Google nie ma czego wyświetlić, więc nie wyświetla nic. Pozycja 220+ nie jest
„słabą pozycją", tylko brakiem kandydata w ogóle.

### Przyczyna wtórna — boilerplate zamiast treści

Fraza pojawia się w serwisie wyłącznie jako **powtarzalny blok CTA** wklejony na
setkach podstron („Sprawdź korepetycje online, dzwoń 512 858 679"). Google
rozpoznaje takie powtarzalne fragmenty szablonu i **dyskontuje je jako boilerplate** —
nie traktuje ich jako sygnału tematycznego strony. Efekt jest gorszy niż zerowy:
sygnał „korepetycje" jest rozmyty równomiernie po całym serwisie, więc żadna
pojedyncza podstrona nie jest dla Google „stroną o korepetycjach". Wszystkie są
stronami o lekturach, które przy okazji mają reklamę.

### Przyczyna trzecia — niedopasowanie intencji

„korepetycje język polski" to zapytanie **komercyjne / transakcyjne** — użytkownik
chce kupić usługę. Cała architektura polskimatura.pl (title, nagłówki, struktura
katalogów, linkowanie wewnętrzne) komunikuje intencję **informacyjną**: opracowania,
testy, epoki. Google sklasyfikował domenę jako zasób edukacyjny, a nie dostawcę
usługi, i pod zapytania usługowe jej nie podstawia.

### Przyczyna czwarta — konkurencja i brak sygnałów usługowych

Cały TOP frazy to marketplace'y z tysiącami profili korepetytorów i bardzo mocnym
profilem linków. Do gry z nimi potrzeba minimum: dedykowanej podstrony, danych
strukturalnych `Service`, wyraźnych sygnałów kontaktu i konwersji. Serwis nie ma
żadnego z tych elementów — nie ma nawet schematu `Organization` z telefonem.

---

## 3. Naprawa — co zostało zrobione w tym repozytorium

### `korepetycje-jezyk-polski/index.html`

Gotowa do wgrania strona docelowa pod adres
`https://polskimatura.pl/korepetycje-jezyk-polski/`. Zawiera:

- **`<title>`** z frazą na początku: „Korepetycje język polski online – matura, olimpiada"
- **`<h1>`** „Korepetycje język polski online" — dokładna fraza, naturalnie
- **`rel=canonical`** na własny adres
- treść odpowiadającą intencji komercyjnej: dla kogo, jak wyglądają zajęcia, zakres,
  cennik, kontakt, FAQ — a nie kolejne opracowanie lektury
- **linkowanie wewnętrzne** do istniejących, potwierdzonych podstron serwisu
  (`/test/egzamin-poprawkowy/`, `/motyw-winy-i-kary.html`, `/polonista/nauka-o-jezyku/`,
  `/epoki/...`, `/autorzy-teksty/baczynski-spojrzenie.html`)
- **JSON-LD**: `Service` + `OfferCatalog`, `Organization` z telefonem i mailem,
  `BreadcrumbList`, `FAQPage` (pytania są też widoczne w treści — warunek konieczny,
  żeby schemat był zgodny z wytycznymi Google)
- warianty frazy rozłożone w treści: „korepetycje z języka polskiego",
  „korepetycje język polski online", „korepetycje maturalne", „lekcje indywidualne"

Strona jest **samodzielna** (style w `<style>`), żeby dało się ją wgrać od razu
i sprawdzić, że działa. Docelowo podmień blok stylów na header/footer i CSS serwisu.

**Świadomie pominięte:** opinie, oceny i `AggregateRating`. Nie mam realnych opinii
uczniów, a wstawienie wymyślonych to zarówno naruszenie wytycznych Google dotyczących
danych strukturalnych, jak i wprowadzanie w błąd. Jeśli masz prawdziwe opinie —
dopisz je i dopiero wtedy dodaj schemat.

**Do uzupełnienia przed publikacją:** realna cena za 60 min w sekcji „Cennik i terminy"
(w pliku jest komentarz `DO UZUPEŁNIENIA`). Ceny w JSON-LD celowo nie ma —
nie wolno jej podawać w danych strukturalnych, jeśli nie ma jej w widocznej treści.

---

## 4. Naprawa — co musisz zrobić po swojej stronie

Sama strona to warunek konieczny, ale nie wystarczający. Kolejność ma znaczenie:

1. **Wgraj katalog** `korepetycje-jezyk-polski/` na serwer, tak aby adres
   `https://polskimatura.pl/korepetycje-jezyk-polski/` zwracał HTTP 200.

2. **Dopisz do `sitemap.xml`:**
   ```xml
   <url>
     <loc>https://polskimatura.pl/korepetycje-jezyk-polski/</loc>
     <changefreq>monthly</changefreq>
     <priority>0.9</priority>
   </url>
   ```

3. **Przebuduj sitewide blok CTA.** To jest ta zmiana, którą najłatwiej pominąć,
   a bez niej efekt będzie o połowę słabszy. Zamiast powtarzać opis usługi na każdej
   podstronie, zostaw krótkie zdanie z **linkiem tekstowym zawierającym frazę**:

   > Potrzebujesz pomocy z tym materiałem?
   > Sprawdź <a href="/korepetycje-jezyk-polski/">korepetycje z języka polskiego online</a>.

   Dzięki temu setki podstron przestają konkurować o frazę i zaczynają **przekazywać
   jej moc na jedną stronę docelową**. Anchor text z frazą jest tu kluczowy.

4. **Dodaj link do korepetycji w głównej nawigacji** (menu górne, nie tylko stopka).
   Pozycja w menu to dla Google mocny sygnał, że to ważna sekcja serwisu.

5. **Zgłoś URL w Google Search Console** → „Sprawdzenie adresu URL" → „Poproś
   o zindeksowanie". Indeksacja: kilka dni. Pierwsze pozycje: 2–6 tygodni.

6. **Zweryfikuj w Search Console** (czego nie mogłem sprawdzić z tego środowiska):
   - czy `robots.txt` nie blokuje czegokolwiek nieoczekiwanie,
   - czy raport „Stan → Strony" nie pokazuje wykluczeń,
   - w „Wyniki wyszukiwania" przefiltruj zapytania po słowie *korepetycje* —
     zobaczysz, czy jest jakiekolwiek wyświetlenie (prawdopodobnie zero, co potwierdzi
     diagnozę).

7. **Załóż i uzupełnij profil Google Business** dla usługi. Znaczna część zapytań
   o korepetycje ma intencję lokalną i wyniki lokalne wchodzą nad organiczne.

---

## 5. Realne oczekiwania

Powiem to wprost, żeby nie było rozczarowania: **na samą frazę „korepetycje język
polski" wejście do TOP 10 jest mało prawdopodobne w krótkim terminie.** To fraza
zdominowana przez marketplace'y, których przewagi (tysiące profili, wiek domeny,
profil linków) nie da się nadrobić jedną podstroną. Ruch z niej jest do tego słabo
konwertujący — użytkownik i tak trafia na listę stu korepetytorów.

Realny plan wygląda inaczej i jest dużo bardziej opłacalny:

- **Fraz z długiego ogona wygrasz szybko**, bo masz pod nie unikalną treść i realną
  przewagę tematyczną. Kandydaci: „korepetycje matura rozszerzona polski",
  „przygotowanie do olimpiady literatury i języka polskiego", „korepetycje przed
  egzaminem poprawkowym z polskiego", „pomoc w wypracowaniu maturalnym online".
  Tu konkurencja jest znikoma, a intencja o wiele mocniejsza.
- **Strona z punktu 3 jest fundamentem pod wszystkie te frazy** — na niej budujesz
  kolejne, węższe podstrony, jeśli któraś z fraz zacznie dawać wyświetlenia.
- **Twoim prawdziwym atutem jest ruch, który już masz.** Setki podstron z lekturami
  odwiedzają maturzyści — czyli dokładnie Twoja grupa docelowa, tylko na wcześniejszym
  etapie. Punkt 3 (przebudowa CTA) zamienia ten istniejący ruch na zapytania o lekcje
  i to zadziała szybciej niż jakiekolwiek pozycjonowanie na frazę główną.

---

## 6. Ograniczenia tej analizy

- Nie udało się pobrać HTML-a polskimatura.pl ani `robots.txt` — polityka sieciowa
  środowiska blokuje ruch wychodzący do tej domeny (HTTP 403 na poziomie proxy,
  zarówno przez `curl`, jak i przez narzędzie pobierające). Wnioski oparte są na
  indeksie Google, który dla tej diagnozy jest źródłem wystarczającym.
- Repozytorium `polskimatura-github` było **puste** (zero commitów), więc nie było
  w nim kodu strony do edycji. Naprawa została przygotowana jako gotowy do wgrania
  plik, a nie jako zmiana w istniejącym szablonie. Jeśli wskażesz, gdzie znajduje się
  źródło serwisu, dostosuję stronę do jego szablonu i wpiszę zmianę CTA bezpośrednio
  w kod.
