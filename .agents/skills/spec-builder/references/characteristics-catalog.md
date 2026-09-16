# Characteristics catalog

A shared vocabulary so that teams name the same quality the same way. Use it only to put a standard name next to what the team wrote; never to choose characteristics for the team.

Based on Ford & Richards, *Fundamentals of Software Architecture*.

## Operational

| Name | Polish | Means | Typical team wording |
|---|---|---|---|
| Availability | Dostępność | the system is up and usable when needed | "nie może leżeć", "24/7", "99,9%" |
| Reliability | Niezawodność | it works correctly over time, doesn't lose data or fail silently | "nie może zgubić zamówienia", "zawsze poprawnie" |
| Recoverability | Odtwarzalność | how fast and how completely it comes back after a failure | "wraca w 5 minut", "backup", "RTO / RPO" |
| Performance | Wydajność | response time and throughput under normal load | "szybko", "poniżej sekundy" |
| Scalability | Skalowalność | handles growth in users, data or requests | "10 razy więcej klientów", "rośnie" |
| Elasticity | Elastyczność obciążeniowa | handles sudden spikes and scales back down | "szczyt", "Black Friday", "start sprzedaży biletów" |
| Robustness | Odporność | keeps working under errors, bad input, failing dependencies | "gdy płatności nie odpowiadają", "tryb awaryjny" |

## Structural

| Name | Polish | Means | Typical team wording |
|---|---|---|---|
| Maintainability | Utrzymywalność | easy to understand and change safely | "łatwo zmienić", "nowy zespół szybko wejdzie" |
| Extensibility | Rozszerzalność | new features or variants can be added without rework | "kolejne kraje", "nowe kanały sprzedaży" |
| Configurability | Konfigurowalność | behaviour changes through configuration, not code | "każdy klient ustawia sam", "reguły per oddział" |
| Interoperability | Interoperabilność | works with other systems through agreed interfaces | "integracja z ...", "API dla partnerów" |
| Deployability | Wdrażalność | releases are frequent, safe and independent | "wdrażamy codziennie", "bez przestojów" |
| Testability | Testowalność | behaviour can be verified automatically and in isolation | "musimy to testować", "symulacja" |
| Portability | Przenośność | runs on different platforms or environments | "chmura i on-premise", "różne urządzenia" |
| Localization | Lokalizacja | languages, currencies, formats, local rules | "wiele języków", "waluty" |

## Cross-cutting

| Name | Polish | Means | Typical team wording |
|---|---|---|---|
| Security | Bezpieczeństwo | protection of data and functions from unauthorised use | "dane osobowe", "płatności", "role" |
| Privacy | Prywatność | handling personal data according to law and consent | "RODO", "prawo do usunięcia danych" |
| Auditability | Audytowalność | who did what and when can be reconstructed | "ślad", "kontrola", "regulator" |
| Legal compliance | Zgodność z prawem | meets regulations and contracts | "ustawa", "norma", "licencja" |
| Usability | Użyteczność | users achieve their goals easily | "bez szkolenia", "seniorzy", "jedną ręką" |
| Accessibility | Dostępność cyfrowa | usable by people with disabilities | "WCAG", "czytnik ekranu" |
| Data consistency | Spójność danych | all parts see the same, correct state | "nie sprzedamy dwa razy", "stan się zgadza" |
| Cost | Koszt | building and running cost within budget | "budżet", "tanio w utrzymaniu" |
| Time to market | Czas wejścia na rynek | available by a fixed date | "pilotaż za 3 miesiące", "przed sezonem" |
