# Weryfikacja przemieszczeń

Proste narzędzie do wizualizacji i wstępnej weryfikacji historii przemieszczeń zwierząt na podstawie danych skopiowanych z IRZ.

Aplikacja działa jako pojedynczy plik HTML otwierany lokalnie w przeglądarce. Nie wymaga instalacji, serwera ani API.

## Status

To jest wersja testowa. Wyniki należy traktować jako wsparcie analizy, a nie jako formalne rozstrzygnięcie. W narzędziu mogą pojawiać się błędy, szczególnie przy nietypowym układzie danych albo sytuacjach, które nie zostały jeszcze opisane regułami.

Dane wklejane do narzędzia nie są wysyłane poza komputer użytkownika.

## Jak uruchomić

1. Pobierz plik `weryfikacja-przemieszczen.html`.
2. Otwórz go dwuklikiem w przeglądarce, np. Edge, Chrome albo Firefox.
3. Skopiuj tabelę zdarzeń z IRZ.
4. Wklej dane w polu `Dane wejściowe`.
5. Kliknij `Analizuj`.

Można też kliknąć `Wczytaj przykład`, żeby zobaczyć demonstracyjne dane z losowymi numerami siedzib stada i dokumentów.

## Co analizuje

Narzędzie próbuje rozpoznać etapy przemieszczeń na podstawie kolumn:

- `L.p`,
- `Typ zdarzenia`,
- `Zgłaszająca działalność`,
- `Komplementarna działalność`,
- `Numer dokumentu`,
- `Data zdarzenia`,
- `Stan zdarzenia`.

Obsługiwane są dane wklejone bezpośrednio z tabeli IRZ, także wtedy, gdy nagłówek kopiuje się jako kilka osobnych linii.

## Obecne funkcje

- wykrywanie par `Wybycie` / `Przybycie`,
- rozpoznawanie zdarzeń `Pasujące`, `Niepasujące` i `Anulowane`,
- wskazywanie brakującego wybycia albo przybycia,
- wykrywanie sytuacji, w której aktywne nieanulowane wybycie może blokować komplementarność dalszych zdarzeń,
- rozpoznawanie duplikatów aktywnych wybyć lub przybyć dla tej samej pary,
- wskazywanie uboju bez odpowiadającego wcześniejszego wybycia,
- prosta wizualizacja łańcucha przemieszczeń w formie osi/rybiej ości,
- lista problemów z sugestią, po której stronie należy wyjaśnić zdarzenie,
- podświetlanie wybranej siedziby stada,
- automatyczne łagodne kolorowanie numerów działalności oraz mocniejsze podświetlenie wszystkich wystąpień po najechaniu,
- filtrowanie widoku zdarzeń po dostępnych numerach dokumentów z możliwością wpisania fragmentu numeru,
- kopiowanie raportu tekstowego,
- pobieranie raportu do pliku `.txt`,
- wczytywanie danych ze schowka lub pliku tekstowego.

## Interpretacja komunikatów

Najczęstsze komunikaty oznaczają:

- `Brak przybycia` - wybycie zostało zgłoszone, ale brakuje odpowiadającego przybycia po stronie działalności docelowej.
- `Brak wybycia` - przybycie zostało zgłoszone, ale brakuje odpowiadającego wybycia po stronie działalności źródłowej.
- `Ubój bez odpowiadającego wybycia` - zarejestrowano przybycie do rzeźni i ubój, ale narzędzie nie widzi wcześniejszego wybycia.
- `Nieanulowane wybycie blokuje zgodność` - dla tej samej pary istnieje anulowane i nadal aktywne wybycie, które może blokować uspójnienie dalszych zdarzeń.
- `Para istnieje, ale może być blokowana wcześniejszym zgłoszeniem` - wybycie i przybycie tworzą parę, ale ich szczegółowy błąd może wynikać z wcześniejszego aktywnego zgłoszenia dla tej samej historii zwierzęcia.
- `Zdarzenie początkowe` - oznakowanie albo zgłoszenie urodzenia jest pojedynczym zdarzeniem i nie wymaga pary wybycie/przybycie.
- `Zdarzenie niepasujące` - obie strony zgłosiły ruch, ale co najmniej jeden dokument wymaga porównania szczegółów.
- `Kilka aktywnych wybyć/przybyć` - dla tej samej pary wykryto więcej niż jeden aktywny dokument po jednej ze stron.

## Praca w zespole

Przy udostępnianiu narzędzia innym osobom warto przekazać krótką zasadę: raport z narzędzia jest pomocą w znalezieniu miejsca, od którego należy zacząć sprawdzanie, a nie końcową decyzją administracyjną.

Jeżeli narzędzie pokaże błędną sugestię albo nie rozpozna oczywistego przypadku, najlepiej zachować:

- skopiowaną tabelę zdarzeń z IRZ,
- informację, który komunikat jest błędny albo czego brakuje,
- oczekiwaną interpretację sprawy.

Na podstawie takich przykładów można dopisywać kolejne reguły analizy.

## Przykład problemu

Jeżeli jeden producent ma dla tej samej pary działalności:

- jedno wybycie anulowane,
- drugie wybycie nadal aktywne i niepasujące,
- brak odpowiadającego przybycia,

narzędzie pokaże sugestię, że aktywne zgłoszenie może blokować zgodność kolejnych zdarzeń i że należy sprawdzić wskazany dokument.

## Ograniczenia

- Narzędzie nie łączy się z IRZ i nie pobiera danych automatycznie.
- Nie sprawdza danych w bazach zewnętrznych.
- Nie jest walidatorem formalnym numerów producenta, dokumentów ani kolczyków.
- Reguły analizy są rozwijane stopniowo na podstawie rzeczywistych przypadków.

## Pliki

- `weryfikacja-przemieszczen.html` - główna aplikacja.
- `README.md` - opis projektu i instrukcja użycia.
