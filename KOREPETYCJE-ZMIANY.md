# Korepetycje — propozycja zmian wizualnych

Przebudowa pierwszego ekranu z oryginalnym portretem Andrzeja Łopaty, graficzne karty siedmiu rodzajów zajęć i dydaktyczny przykład budowania argumentu na podstawie *Lalki*. Układ ma warianty dla telefonu, tabletu i komputera. Menu mobilne otrzymało przycisk obsługiwany z klawiatury i stan aria-expanded.

Repozytorium nie zawierało publicznego pliku `korepetycje.html`. Dodany plik bazuje na pobranej stronie https://polskimatura.pl/korepetycje.html (SHA256 oryginału: bb2ee32570b90c6b60c559ba00e7ec0b68828f63d0964054ac5170c04b888d30). Istniejący landing `korepetycje-jezyk-polski/index.html` pozostaje osobnym dokumentem.

## Pliki do późniejszego wdrożenia

- `korepetycje.html` — katalog główny domeny.
- `assets/korepetycje/korepetycje-2026.css` — zachować ścieżkę.
- `assets/korepetycje/andrzej-lopata.jpg` — zachować ścieżkę.

Przed ręcznym wdrożeniem wykonać kopię dotychczasowego pliku na hostingu i porównać go z aktualną stroną: równoległe zmiany mogą wymagać scalenia. Nie podmieniać katalogu korepetycje, backendu formularza, konfiguracji hostingu ani pliku zgoda-cookies.js. Ten commit nie publikuje zmian na stronie.

## Sprawdzenie

Porównanie kodu potwierdziło identyczny formularz, skrypty i sekcję cennika względem pobranego oryginału. Zachowano title, opis, canonical i dane JSON-LD. Sprawdzono unikalność ID, odnośniki do sekcji, pojedyncze H1 i main oraz zgodność zdjęcia z dostarczonym JPEG.

Podgląd HTML jest przeznaczony do oceny wyglądu i ma wyłączoną wysyłkę zgłoszeń. Polityka narzędzia przeglądarkowego zablokowała otwarcie lokalnego podglądu; nie wykonano testu renderowania w rzeczywistej przeglądarce ani testowej wysyłki formularza. Przed publikacją sprawdzić wygląd na telefonie i komputerze, menu oraz formularz na hostingu testowym.
