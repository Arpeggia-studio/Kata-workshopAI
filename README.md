# Kata-workshopAI

Mini framework na warsztat architektoniczny. **Wy myślicie, pytacie i decydujecie. AI tylko zadaje wam trudne pytania i porządkuje to, co zapisaliście.**

Działa w Claude Code i w Codex CLI. Cała wasza praca ląduje w folderze `zadanie/`.

---

## 1. Przygotowanie (10 minut, najlepiej przed warsztatem)

1. **Zainstaluj** Claude Code albo Codex CLI i zaloguj się.
2. **Sklonuj repozytorium** i wejdź do niego:
   ```
   git clone <adres-repozytorium>
   cd Kata-workshopAI
   ```
3. **Uruchom agenta w głównym katalogu repozytorium** (nie w `zadanie/`, bo wtedy agent nie zobaczy skilli):
   ```
   claude
   ```
   albo
   ```
   codex
   ```
4. **Sprawdź, że widać skille.**
   - Claude Code: wpisz `/` i sprawdź, że na liście są `grill-me`, `spec-builder`, `adr-builder`.
   - Codex: zapytaj „Jakie skille widzisz w tym projekcie?”.
5. **Podłącz Miro** (opcjonalnie, ale wygodnie). Wtedy AI przeczyta waszą tablicę bezpośrednio.
   - Claude Code, w terminalu poza agentem:
     ```
     claude mcp add --transport http miro https://mcp.miro.com/
     ```
     Potem w Claude Code wpisz `/mcp`, wybierz `miro` i zaloguj się w przeglądarce. Jeśli masz Miro podłączone jako connector na claude.ai, ten krok możesz pominąć.
   - Codex, w terminalu:
     ```
     codex mcp add miro --url https://mcp.miro.com/
     codex mcp login miro
     ```

   Nie macie Miro MCP? Nic straconego: wrzucicie obrazek tablicy (krok 4).

---

## 2. Co jest w folderze `zadanie/`

| Plik / folder | Kto pisze | Co tam jest |
|---|---|---|
| `zadanie/zadanie.md` | wy (wklejacie) | treść zadania od prowadzących |
| `zadanie/notatki.md` | **wy** | wasze pytania, odpowiedzi, konteksty, charakterystyki, decyzje. **Najważniejszy plik.** |
| `zadanie/miro.md` | wy | link do tablicy Event Storming (i legenda kolorów, jeśli inna niż standardowa) |
| `zadanie/event-storming/` | wy | eksport tablicy jako PNG, jeśli nie macie Miro MCP |
| `zadanie/grill-me.md` | AI (`grill-me`) | pytania, które AI wam zadało, ponumerowane Q1, Q2, ... |
| `zadanie/spec/01-prd.md` | AI (`spec-builder`) | PRD: problem, aktorzy, zakres, wymagania, ograniczenia, założenia |
| `zadanie/spec/02-domain.md` | AI (`spec-builder`) | bounded contexty, mapa kontekstów, moduły |
| `zadanie/spec/03-characteristics.md` | AI (`spec-builder`) | charakterystyki architektury, top 3, trade-offy |
| `zadanie/adr/` | AI (`adr-builder`) | decyzje architektoniczne (ADR) |

**Zasada:** wy piszecie w `notatki.md`, AI pisze w `grill-me.md`, `spec/` i `adr/`. Jeśli coś w `spec/` jest źle, poprawcie notatkę i uruchomcie `spec-builder` ponownie.

---

## 3. Krok po kroku

### Krok 1: Start (5 minut)

1. Wklejcie treść zadania do **`zadanie/zadanie.md`**.
2. Wpiszcie nazwę zespołu i uczestników na górze **`zadanie/notatki.md`**.

### Krok 2: Myślicie sami (ok. 60 minut, bez AI)

1. Czytajcie zadanie i zadawajcie pytania. Zapisujcie je w **`zadanie/notatki.md`**, w sekcji „Nasze pytania i odpowiedzi”, razem z odpowiedziami (także „nie wiemy”).
2. Zróbcie **Event Storming na Miro**: zdarzenia, komendy, aktorzy, polityki, systemy zewnętrzne, hotspoty. Jeśli wyznaczycie granice kontekstów, narysujcie je ramkami i nazwijcie.
3. Wnioski o domenie, charakterystykach i decyzjach dopisujcie od razu do odpowiednich sekcji `notatki.md`.

Jak pisać notatki, żeby AI dobrze je rozłożyło: krótko, jedna myśl w punkcie, z uzasadnieniem.

```
- Gość może zarezerwować konkretny pokój, nie tylko typ pokoju
- Szczyt: 5 tys. rezerwacji na godzinę przy starcie sezonu
- Bounded context Rezerwacje (core): przyjmuje i potwierdza rezerwacje
- Najważniejsza jest dostępność, bo w sezonie każda minuta przestoju to utracona sprzedaż
- Wybraliśmy jedną bazę dla przydziału pokoi, bo nie może być podwójnej rezerwacji
- Nie wiemy: kto obsługuje zwroty, hotel czy my
```

### Krok 3: Pokażcie AI tablicę

Wybierzcie **jedną** opcję:

- **A. Link (macie Miro MCP):** wklejcie link do tablicy do **`zadanie/miro.md`**. Tablica musi być udostępniona kontu, którym zalogowaliście się do Miro w agencie.
- **B. Obrazek (bez Miro MCP):** wyeksportujcie tablicę z Miro jako PNG i wrzućcie do **`zadanie/event-storming/`**. Przy dużej tablicy eksportujcie ramki osobno (np. `01-rezerwacja.png`, `02-pobyt.png`), bo na jednym dużym obrazku tekst karteczek jest nieczytelny.

### Krok 4: `grill-me`, czyli AI was challenguje

W agencie wpiszcie:

| Claude Code | Codex |
|---|---|
| `/grill-me` | `Użyj skilla grill-me.` |

AI przeczyta `zadanie.md`, `notatki.md`, tablicę (link albo obrazki) i zada 15-25 pytań w trzech grupach: czego nie zapytaliście, jakie założenia warto podważyć, jak porównać warianty. Pytania zobaczycie w czacie i w **`zadanie/grill-me.md`**.

Co dalej:

1. Zacznijcie od 5 pytań oznaczonych „Zacznijcie od tych 5”.
2. Dyskutujcie w zespole. **AI nie odpowie za was i nie oceni odpowiedzi.**
3. Odpowiedzi zapiszcie w **`zadanie/notatki.md`**, w sekcji „Odpowiedzi na grill-me”, z numerem pytania:
   ```
   - Q3: płatność potwierdzana przed przydziałem pokoju, blokada pokoju na 15 minut
   - Q7: nie wiemy, zapytamy prowadzących
   ```
4. Chcecie kolejną rundę? Zmieńcie tablicę lub notatki i wpiszcie znowu `/grill-me`. Możecie zawęzić: `/grill-me tylko płatności`, `/grill-me więcej o wariantach`.

### Krok 5: `spec-builder`, czyli porządkowanie notatek

| Claude Code | Codex |
|---|---|
| `/spec-builder` | `Użyj skilla spec-builder.` |

AI rozłoży wasze notatki (i tablicę) do trzech plików w **`zadanie/spec/`**: PRD, domena, charakterystyki. **O nic nie pyta i nic nie dopisuje od siebie.** Czego nie ma w notatkach, tego nie będzie w specyfikacji; taka sekcja dostaje „Brak w notatkach.”.

W odpowiedzi dostaniecie raport:

- co dodało i zmieniło (z numerami, np. `FR-05`, `BC-02`, `AC-01`),
- które sekcje są puste,
- niespójności między plikami (np. wymaganie bez modułu),
- notatki, które wyglądają na decyzje do zapisania w ADR,
- notatki, których nie umiało przypisać.

Co zrobić z raportem: to wy decydujecie, czy pusta sekcja lub niespójność to problem. Jeśli tak, dopiszcie notatkę i uruchomcie `/spec-builder` ponownie. Numery (`FR-01` itd.) zostają te same, więc możecie się na nie powoływać w notatkach („Moduł Kuchnia realizuje FR-03 i FR-04”).

Tylko jeden plik: `/spec-builder tylko charakterystyki`.

### Krok 6: `adr-builder`, czyli zapis decyzji

Dla każdej decyzji z sekcji „Decyzje” (albo z raportu `spec-builder`):

| Claude Code | Codex |
|---|---|
| `/adr-builder jedna baza dla przydziału pokoi` | `Użyj skilla adr-builder dla decyzji: jedna baza dla przydziału pokoi.` |

AI weźmie kontekst z notatek i specyfikacji, zapyta was o brakujące alternatywy i koszty, a potem zapisze ADR w **`zadanie/adr/0001-....md`**. Jeśli jeszcze nie zdecydowaliście, AI odeśle was do dyskusji (albo do `grill-me`), zamiast wybrać za was.

Jedna decyzja = jeden ADR.

### Krok 7: Prezentacja

Macie gotowe materiały:

- `zadanie/spec/01-prd.md`: co budujecie i dla kogo
- `zadanie/spec/02-domain.md`: jak podzieliliście domenę
- `zadanie/spec/03-characteristics.md`: co jest najważniejsze i dlaczego
- `zadanie/adr/`: jakie decyzje podjęliście i czym za nie płacicie
- `zadanie/grill-me.md` + `notatki.md`: jakie trudne pytania padły i jak na nie odpowiedzieliście

---

## 4. Ściąga

| Chcę | Claude Code | Codex |
|---|---|---|
| dostać trudne pytania | `/grill-me` | `Użyj skilla grill-me.` |
| pytania tylko o jeden obszar | `/grill-me tylko <obszar>` | `Użyj skilla grill-me, tylko <obszar>.` |
| zapisać notatki do specyfikacji | `/spec-builder` | `Użyj skilla spec-builder.` |
| zaktualizować jeden plik specyfikacji | `/spec-builder tylko prd` | `Użyj skilla spec-builder, tylko PRD.` |
| zapisać decyzję | `/adr-builder <decyzja>` | `Użyj skilla adr-builder dla decyzji: <decyzja>.` |

Cykl pracy: **notatki → `grill-me` → odpowiedzi w notatkach → `spec-builder` → `adr-builder`**, i od nowa, ile razy chcecie.


---

## 5. Gdy coś nie działa

| Problem | Co zrobić |
|---|---|
| Agent nie widzi skilli | Uruchomcie `claude` / `codex` w głównym katalogu repozytorium, nie w `zadanie/`. |
| AI mówi, że nie ma zadania | Sprawdźcie, czy treść jest w `zadanie/zadanie.md` (poza komentarzem `<!-- -->`). |
| AI nie może otworzyć tablicy | Udostępnijcie tablicę kontu z Miro MCP (w Claude Code sprawdźcie `/mcp`) albo wrzućcie PNG do `zadanie/event-storming/`. |
| AI nie czyta karteczek z obrazka | Eksportujcie mniejsze fragmenty (ramka po ramce) w wyższej rozdzielczości. |
| W `spec/` jest coś źle | Poprawcie lub dopiszcie notatkę w `notatki.md` („zmiana: ...”) i uruchomcie `/spec-builder` ponownie. |
| AI coś doradza albo ocenia | Nie powinno. Przypomnijcie mu: „Tylko pytania / tylko zapisuj z notatek.” i dajcie znać prowadzącym. |
| Chcemy zacząć od nowa | `git checkout -- zadanie` przywraca pliki do ostatniego commita. |

---

