# Kafka od środka

Kurs Apache Kafka i Spring Kafka oparty na eksperymentach na lokalnym klastrze.

## Weryfikowalność

Projekt opiera się na weryfikowalnych eksperymentach. Każde istotne twierdzenie o Kafce i Spring Kafka ma źródło: dokumentację przypiętej wersji, KIP, specyfikację protokołu, kod źródłowy albo eksperyment z katalogu `experiments/`.

Każdy artefakt i rysunek ma etykietę: `OBSERVED` (zaobserwowany na klastrze), `GENERATED` (wynik uruchomienia testu lub skryptu) albo `ILLUSTRATIVE` (przykład objaśniający, który nie pochodzi z uruchomienia).

Każdy eksperyment ma własny README według szablonu `docs/templates/experiment-README.md`.

Szczegółowe zasady: [`docs/evidence-policy.md`](docs/evidence-policy.md).
