# Wdrożenie na az.pl — `korepetycje-jezyk-polski.zip`

Archiwum zawiera jeden katalog i jeden plik:

```
korepetycje-jezyk-polski/
└── index.html
```

Efekt docelowy: `https://polskimatura.pl/korepetycje-jezyk-polski/` zwraca HTTP 200.

---

## Krok 1 — wgranie przez Menedżer plików

1. Zaloguj się do panelu az.pl → **Hosting** → **Menedżer plików** (albo klient FTP).
2. Wejdź do katalogu, w którym leży obecna strona główna serwisu — czyli tam, gdzie
   widzisz `index.html` / `sitemap.xml` / katalogi `epoki`, `test`, `autorzy-teksty`.
   Na az.pl jest to zwykle `public_html/`, a przy kilku domenach na koncie:
   `domains/polskimatura.pl/public_html/`.
   **Kluczowe:** rozpakuj dokładnie w tym katalogu, nie piętro wyżej.
3. Wgraj `korepetycje-jezyk-polski.zip`.
4. Zaznacz plik → **Rozpakuj / Wypakuj** (Extract).
5. Skasuj `.zip` z serwera — nie musi tam zostać.

Archiwum ma katalog w środku, więc po rozpakowaniu powstanie
`public_html/korepetycje-jezyk-polski/index.html`. Nic nie nadpisuje istniejących
plików serwisu.

**Alternatywa przez FTP** (FileZilla): przeciągnij cały katalog
`korepetycje-jezyk-polski` do `public_html/` — bez pakowania.

## Krok 2 — sprawdzenie

Wejdź na `https://polskimatura.pl/korepetycje-jezyk-polski/`.

- Strona się otwiera → OK, przejdź dalej.
- **404** → rozpakowałeś w złym katalogu. Sprawdź, czy ścieżka to na pewno ten sam
  katalog, w którym leży `index.html` strony głównej.
- **Otwiera się lista plików zamiast strony** → serwer nie podaje `index.html` jako
  domyślnego. Wtedy albo użyj adresu z pełną nazwą pliku, albo dopisz w `.htaccess`
  w katalogu strony: `DirectoryIndex index.html`.
- **Krzaki zamiast polskich znaków** → plik jest w UTF-8 i ma poprawny `<meta charset>`;
  jeśli mimo to są krzaki, serwer wymusza inne kodowanie — dopisz w `.htaccess`:
  `AddDefaultCharset UTF-8`.

## Krok 3 — po wgraniu (bez tego strona nie zacznie rankować)

1. **`sitemap.xml`** — dopisz przed `</urlset>`:
   ```xml
   <url>
     <loc>https://polskimatura.pl/korepetycje-jezyk-polski/</loc>
     <changefreq>monthly</changefreq>
     <priority>0.9</priority>
   </url>
   ```

2. **Przebuduj sitewide blok CTA.** Zamiast powtarzanego opisu usługi z telefonem
   na każdej podstronie — krótkie zdanie z linkiem:
   ```html
   <p>Potrzebujesz pomocy z tym materiałem?
   Sprawdź <a href="/korepetycje-jezyk-polski/">korepetycje z języka polskiego online</a>.</p>
   ```
   To najważniejsza zmiana po stronie serwisu — bez niej podstrony dalej konkurują
   o frazę zamiast przekazywać jej moc na stronę docelową.

3. **Dodaj pozycję „Korepetycje" do górnego menu**, nie tylko do stopki.

4. **Google Search Console** → Sprawdzenie adresu URL → wklej
   `https://polskimatura.pl/korepetycje-jezyk-polski/` → **Poproś o zindeksowanie**.

5. **Uzupełnij cenę** w sekcji „Cennik i terminy" — w pliku jest komentarz
   `DO UZUPEŁNIENIA PRZED PUBLIKACJĄ`. Jeśli wpiszesz konkretną kwotę, dopisz ją też
   w JSON-LD (jest tam instrukcja). Ceny w danych strukturalnych nie wolno podawać,
   jeśli nie ma jej w widocznej treści strony.

## Uwaga o wyglądzie

Plik jest samodzielny — style siedzą w `<style>` w `<head>`, żeby działał od razu
po wgraniu, bez zależności od CSS serwisu. Będzie więc wyglądał podobnie, ale nie
identycznie jak reszta polskimatura.pl i **nie będzie miał Twojej nawigacji**.

Docelowo: wytnij blok `<style>`, wstaw wspólny header i footer w miejsca oznaczone
komentarzami `=== MIEJSCE NA WSPÓLNY HEADER ===` / `=== ...FOOTER ===` i podepnij
arkusz CSS serwisu.

Nie zmieniaj przy tym: `<title>`, `<meta name="description">`, `<link rel="canonical">`,
`<h1>` ani bloków JSON-LD — to one odpowiadają za widoczność na frazę.
