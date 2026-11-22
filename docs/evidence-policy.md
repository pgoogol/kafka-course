# Kontrakt prawdziwości i źródeł (Evidence Policy)

Wersja dokumentu: 1.0

## 1. Cel

Ten dokument określa, na jakiej podstawie wolno w projekcie formułować twierdzenia techniczne o Apache Kafka i Spring Kafka oraz tworzyć materiały edukacyjne. Chodzi o to, żeby żaden materiał nie opierał się na przekonującym, ale niesprawdzonym opisie.

Dokument obowiązuje we wszystkich ośmiu warstwach kursu, we wszystkich eksperymentach i materiałach graficznych.

## 2. Zakres

Zasady dotyczą:
- wyjaśnień w rozmowach i notatkach,
- eksperymentów w katalogu `experiments/`,
- artefaktów (zrzuty, logi, wyniki CLI, metryki, ruch sieciowy, wyniki testów i pomiarów),
- rysunków Excalidraw, animacji i widgetów.

## 3. Dopuszczalne źródła

Istotne twierdzenie techniczne musi opierać się na co najmniej jednym z poniższych źródeł. Każde z nich dowodzi czegoś innego:

| Źródło | Czego dowodzi | Na co uważać |
|---|---|---|
| Oficjalna dokumentacja przypiętej wersji | Zachowanie i gwarancje, które projekt deklaruje publicznie | Dokumentacja bywa nieaktualna albo nieprecyzyjna w szczegółach |
| KIP | Motywacja, historia i zamierzony projekt mechanizmu | KIP opisuje propozycję. Trzeba sprawdzić status i wersję, w której wszedł, bo implementacja mogła odejść od tekstu |
| Specyfikacja protokołu | Format żądań, odpowiedzi i danych na dysku | Opisuje format, nie zachowanie przy awariach |
| Kod źródłowy przypiętej wersji | Faktyczna implementacja w tej wersji | Szczegół implementacji może się zmienić w kolejnej wersji bez ogłoszenia |
| Eksperyment na naszym klastrze | Zachowanie w naszej konfiguracji i środowisku | Wynik dotyczy tej konfiguracji. Nie uogólniamy go bez źródła z wierszy powyżej |

Wiedza z pamięci modelu językowego, artykuły na blogach i odpowiedzi na forach nie są źródłem. Mogą podsunąć hipotezę albo miejsce, w którym warto szukać.

## 4. Gwarancja a szczegół implementacji

Przy każdym istotnym twierdzeniu zaznaczamy, czym ono jest:

- **Gwarancja API**: zachowanie opisane w dokumentacji, javadoc albo przyjętym KIP-ie. Można na nim opierać kod aplikacji.
- **Szczegół implementacji**: zachowanie widoczne w kodzie albo w eksperymencie, ale niezadeklarowane publicznie. Pomaga zrozumieć mechanizm, ale aplikacja nie powinna na nim polegać.

## 5. Status twierdzeń

- Twierdzenie ze wskazanym źródłem jest pełnoprawną częścią materiału.
- Twierdzenie bez źródła oznaczamy `[DO WERYFIKACJI]` i dopisujemy, jak je sprawdzić (dokument, plik w kodzie albo eksperyment).
- Nazwy klas, metod i właściwości konfiguracyjnych podane z pamięci mają status `[DO WERYFIKACJI]`, dopóki nie mają odnośnika do kodu albo dokumentacji przypiętej wersji.

## 6. Odnośniki do kodu

Odnośnik do kodu zawiera:
- repozytorium i wersję (tag wydania),
- ścieżkę pliku,
- klasę i metodę,
- link do tagu na GitHubie, najlepiej z numerami linii.

Nie linkujemy do `trunk` ani `main`, bo ich treść się zmienia.

Format zapisu:

```
Kafka <wersja> · clients/src/main/java/.../RecordAccumulator.java · RecordAccumulator#append
https://github.com/apache/kafka/blob/<tag>/<ścieżka>#L<od>-L<do>
```

## 7. Etykiety materiałów

Każdy artefakt i każdy materiał graficzny ma dokładnie jedną etykietę.

| Etykieta | Znaczenie | Przykłady |
|---|---|---|
| `OBSERVED` | Wynik zaobserwowany ręcznie na działającym klastrze | Zrzut segmentu, log DEBUG, wynik CLI, metryka JMX, przechwycony ruch |
| `GENERATED` | Wynik rzeczywistego uruchomienia testu albo skryptu z repozytorium | Raport testu na Testcontainers, wynik perf-testu zapisany przez skrypt |
| `ILLUSTRATIVE` | Przykład przygotowany do wyjaśnienia, który nie pochodzi z uruchomienia | Wymyślony zrzut, przykładowe offsety, szkic przed eksperymentem |

Reguły:
1. Materiał `ILLUSTRATIVE` nigdy nie jest przedstawiany jako wynik eksperymentu.
2. Wszystko, co napisał asystent AI jako przykładowy wynik, ma etykietę `ILLUSTRATIVE`. `GENERATED` oznacza wynik prawdziwego uruchomienia, a nie tekst wygenerowany przez model.
3. Oczekiwane artefakty zapisane przed eksperymentem są częścią hipotezy, a nie artefaktem.
4. Rysunek dziedziczy etykietę materiału, na którym się opiera. Na rysunku umieszczamy etykietę i ścieżkę do artefaktu źródłowego, na przykład w rogu: `OBSERVED · experiments/L1-01-segment-dump/artifacts/raw/dump.txt`.
5. Rysunek łączący artefakty o różnych etykietach dostaje najsłabszą z nich (`ILLUSTRATIVE` < `GENERATED` < `OBSERVED`) albo dzieli się na oznaczone części.

## 8. Praca z asystentem AI

Zasady zależą od tego, czy asystent ma dostęp do klastra i repozytorium.

### 8.1. Bez dostępu (np. czat)

Asystent:
- przygotowuje komendy, skrypty i instrukcje, które pozwalają uzyskać wynik samodzielnie,
- nie twierdzi, że eksperyment został wykonany,
- nie podaje wyników eksperymentu, dopóki nie zostaną wklejone,
- analizuje i interpretuje dopiero wklejone artefakty.

### 8.2. Z dostępem (np. Claude Code w katalogu repozytorium)

Asystent:
- uruchamia komendy i testy sam, ale tylko te zapisane w eksperymencie (`run.sh`, testy). Komenda wykonana ręcznie trafia do README eksperymentu przed uznaniem wyniku,
- zapisuje wyjście do `artifacts/raw/` bez skracania, filtrowania i poprawiania. Skrócone wersje do omówienia powstają skryptem w `artifacts/derived/`,
- oznacza wynik jako `OBSERVED` albo `GENERATED` tylko wtedy, gdy plik w `artifacts/raw/` naprawdę powstał z uruchomienia,
- przy nieudanym uruchomieniu zapisuje błąd jako artefakt i nie podstawia oczekiwanego wyniku,
- nie zmienia konfiguracji, wersji ani kodu eksperymentu po to, żeby wynik zgadzał się z hipotezą. Każda zmiana jest zapisana w README z powodem, a eksperyment jest uruchamiany ponownie,
- nie wykonuje operacji niszczących poza środowiskiem eksperymentu (np. usuwania danych spoza `experiments/` albo wolumenów innych projektów).

### 8.3. W obu trybach

- Asystent mówi wprost, w którym trybie pracuje.
- Interpretacja asystenta nie jest artefaktem. Artefaktem jest tylko plik z wynikiem uruchomienia.

## 9. Przechowywanie artefaktów

- Surowe artefakty trafiają do `artifacts/raw/` danego eksperymentu i nie są edytowane ręcznie.
- Przetworzone dane (wycinki, tabele, dane do wykresów) trafiają do `artifacts/derived/` i powstają skryptem zapisanym w eksperymencie.
- Przy każdym artefakcie zapisujemy w README eksperymentu: etykietę, ścieżkę, komendę, która go wytworzyła, datę i wersje komponentów.
- Bardzo duże pliki (np. pełne przechwycenia ruchu) mogą być poza repozytorium, ale README podaje, jak je odtworzyć.

## 10. Postępowanie przy rozbieżnościach

Gdy dokumentacja, KIP, kod i wynik eksperymentu wydają się sprzeczne:

1. Zachowaj wynik eksperymentu w niezmienionej postaci.
2. Sprawdź konfigurację i wersje wszystkich komponentów.
3. Przeanalizuj logi i kod źródłowy przypiętej wersji.
4. Wyjaśnij przyczynę rozbieżności.
5. Określ, jakie zachowanie faktycznie gwarantuje przypięta wersja.

Nie dopasowujemy wyniku eksperymentu do przygotowanej wcześniej teorii. Rozbieżność i jej wyjaśnienie zapisujemy w sekcji „Rozbieżności” README eksperymentu. Jeśli przyczyny nie udało się ustalić, zapisujemy to wprost.

## 11. Powtarzalność

Każdy eksperyment da się uruchomić od zera. Jego README powstaje według szablonu `docs/templates/experiment-README.md`.

Wersje komponentów przypinamy w jednym miejscu (`versions.env`), a eksperymenty z niego korzystają. Jeśli eksperyment wymaga innej wersji, nadpisuje ją jawnie i podaje powód.

### Benchmarki

Przy pomiarach wydajności zapisujemy także warunki pomiaru:
- sprzęt i zasoby przydzielone kontenerom,
- wersję JVM i ustawienia pamięci,
- liczbę przebiegów i rozgrzewkę,
- rozmiar i liczbę wiadomości,
- medianę i rozrzut wyników.

Nie oczekujemy identycznych liczb przy każdym uruchomieniu. Oczekujemy tego samego kierunku i rzędu wielkości zmian.

## 12. Przegląd zewnętrzny

Materiały mogą trafiać do niezależnego recenzenta (np. innego modelu językowego), który szuka błędów, nieścisłości i twierdzeń bez dowodów. Recenzent dostaje polecenie z `docs/review-prompt.md`.

### 12.1. Co dostaje recenzent

- `docs/evidence-policy.md`,
- `versions.env`,
- README eksperymentu,
- surowe artefakty z `artifacts/raw/`, nie tylko wersje przetworzone,
- materiał do sprawdzenia (wyjaśnienie, rysunek, notatkę).

### 12.2. Status uwag recenzenta

- Uwaga recenzenta nie jest źródłem ani artefaktem. Jest hipotezą do sprawdzenia, tak jak twierdzenie `[DO WERYFIKACJI]`.
- Recenzent podlega tym samym zasadom co asystent: jego twierdzenia wymagają źródła z punktu 3.
- Zgodność dwóch modeli nie jest dowodem. Rozstrzyga źródło albo eksperyment.

### 12.3. Rozpatrywanie uwag

Każda uwaga dostaje jeden wynik:

| Wynik | Znaczenie | Co dalej |
|---|---|---|
| `PRZYJĘTA` | Źródło albo artefakt potwierdza uwagę | Poprawka materiału z odnośnikiem do źródła |
| `ODRZUCONA` | Źródło albo artefakt przeczy uwadze | Zapis, które źródło jej przeczy |
| `WYMAGA EKSPERYMENTU` | Nie da się rozstrzygnąć bez uruchomienia | Nowy eksperyment albo rozszerzenie istniejącego |
| `NIEROZSTRZYGNIĘTA` | Brak źródła w obie strony | Twierdzenie dostaje `[DO WERYFIKACJI]` |

Uwagi i wyniki zapisujemy w sekcji „Przegląd” README eksperymentu. Uwagi dotyczące materiałów spoza eksperymentów trafiają do `docs/reviews/RRRR-MM-DD-<temat>.md`.

Uwag nie przyjmuje się hurtowo. Każdą rozpatruje się osobno.

## 13. Lista kontrolna przed uznaniem materiału za gotowy

- [ ] Każde istotne twierdzenie ma źródło albo oznaczenie `[DO WERYFIKACJI]`.
- [ ] Odnośniki do kodu wskazują tag przypiętej wersji.
- [ ] Zaznaczono, co jest gwarancją API, a co szczegółem implementacji.
- [ ] Każdy artefakt i rysunek ma etykietę i ścieżkę do źródła.
- [ ] Żaden materiał `ILLUSTRATIVE` nie udaje wyniku eksperymentu.
- [ ] Rozbieżności są opisane albo wyjaśnione.
- [ ] README eksperymentu ma wszystkie sekcje z szablonu.
- [ ] Jeśli materiał przeszedł przegląd zewnętrzny, każda uwaga ma wynik z punktu 12.3.
