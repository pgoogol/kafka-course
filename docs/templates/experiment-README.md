# <ID>: <krótki tytuł>

<!-- ID w formacie L<warstwa>-<numer>-<nazwa>, np. L1-01-segment-dump -->

## Cel

Jakie pytanie rozstrzyga ten eksperyment i z którym niezmiennikiem warstwy się wiąże.

## Hipoteza

Czego się spodziewam, zapisane przed uruchomieniem.

### Oczekiwane artefakty

Jakie artefakty powinny powstać i co powinno w nich być widać. To część hipotezy, nie wynik.

## Środowisko

- Wersje: z `versions.env` (wypisz użyte wartości). Nadpisania: <brak / jakie i dlaczego>
- Konfiguracja brokerów, topiców i klientów istotna dla eksperymentu:

```
<konfiguracja>
```

- Warunki pomiaru (tylko benchmarki): sprzęt, zasoby kontenerów, JVM, liczba przebiegów, rozgrzewka, rozmiar wiadomości.

## Przygotowanie

Kroki od czystego środowiska do stanu gotowego do uruchomienia.

```bash
<komendy>
```

## Uruchomienie

Dokładne komendy albo testy.

```bash
<komendy>
```

## Artefakty

| Etykieta | Ścieżka | Komenda, która go wytworzyła | Data | Uwagi |
|---|---|---|---|---|
| OBSERVED / GENERATED | `artifacts/raw/...` | `...` | RRRR-MM-DD | |

Surowe pliki w `artifacts/raw/` nie są edytowane. Przetworzone dane w `artifacts/derived/` powstają skryptem: `<skrypt>`.

## Analiza

Interpretacja wyników na podstawie artefaktów i kodu. Przy każdym istotnym twierdzeniu: źródło i informacja, czy to gwarancja API, czy szczegół implementacji.

## Rozbieżności

Różnice między hipotezą, dokumentacją, KIP-em, kodem i wynikiem oraz ich wyjaśnienie według `docs/evidence-policy.md`, punkt 10. Jeśli brak: „Brak”.

## Ograniczenia

Czego ten eksperyment nie pokazuje i na jakie konfiguracje nie wolno uogólniać wyniku.

## Materiały

| Plik | Etykieta | Artefakt źródłowy |
|---|---|---|
| `drawings/....excalidraw` | | `artifacts/raw/...` |

## Przegląd

Uwagi z przeglądu zewnętrznego według `docs/evidence-policy.md`, punkt 12. Jeśli przeglądu nie było: „Brak”.

| Data | Recenzent | Uwaga | Wynik | Źródło rozstrzygnięcia |
|---|---|---|---|---|
| RRRR-MM-DD | | | PRZYJĘTA / ODRZUCONA / WYMAGA EKSPERYMENTU / NIEROZSTRZYGNIĘTA | |

## Źródła

- Dokumentacja: <link do wersji>
- KIP: <numer, status, wersja wejścia>
- Specyfikacja protokołu: <link>
- Kod: <repozytorium · tag · plik · klasa#metoda · link>
