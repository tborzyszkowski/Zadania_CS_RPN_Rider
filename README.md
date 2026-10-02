# Odwrotna Notacja Polska

| Termin oddania      | Punkty     |
|---------------------|:-----------|
|    25.10.2026 23:00 |   10       |

--- 
Przekroczenie terminu o **n** zajęć wiąże się z karą:
- punkty uzyskania za realizację zadania są dzielone przez **2<sup>n</sup>**.

--- 

## Zadanie 1 (Faza RED – Testy jednostkowe)

Opierając się na dostarczonej definicji stosu, przygotuj w pliku `RPNTest` zestaw testów jednostkowych dla metody `evalRPN` z klasy `RPN`. Metoda ta przyjmuje jako argument napis (`string`) zawierający wyrażenie w **Odwrotnej Notacji Polskiej (RPN)** i zwraca wynik jego obliczenia.

### Wymagania funkcjonalne do przetestowania:

1. **Systemy liczbowe (Przedrostki liczb):**
    - **Dziesiętny (`D` lub brak przedrostka):** np. `D10` = 10, `12` = 12.
    - **Dwójkowy (`B`):** np. `B101` = 5.
    - **Szesnastkowy (`#`):** np. `#AB` = 171.
    - **Złożone wyrażenia mieszane:** np. `#BA D13 +` = 199.


2. **Operacje dwuargumentowe:**
    - Dodawanie (`+`), odejmowanie (`-`), mnożenie (`*`).
    - Dzielenie (`/`) – wymaga osobnego przetestowania poprawnego dzielenia oraz zgłaszania błędu przy próbie dzielenia przez zero.


3. **Operacje jednoargumentowe:**
    - Wartość bezwzględna (np. `ABS`) oraz silnia (np. `!`).
    - *Przykład:* `B101 !` = 120.


4. **Obsługa błędów i niepoprawnych składniowo wyrażeń (Sytuacje wyjątkowe):**
    - **Za dużo argumentów / niedokończone wyrażenie:** np. `1 2` (po zakończeniu obliczeń na stosie zostaje więcej niż jeden element).
    - **Za mało argumentów dla operatora:** np. `1 +` lub `ABS` na pustym stosie.
    - **Dzielenie przez zero:** np. `5 0 /`.
    - **Błędny format liczby w danym systemie:** np. `B102` (cyfra `2` w systemie binarnym) lub `#XY`.
    - **Nierozpoznany symbol / operator.**



> **Uwaga:** Testy powinny jednoznacznie weryfikować zarówno poprawne wyniki zwracane przez funkcję, jak i rzucanie odpowiednich wyjątków (np. `ArgumentException`, `DivideByZeroException` lub dedykowego wyjątku błędu RPN) w przypadku niepoprawnych danych wejściowych.

---

## Zadanie 2 (Faza GREEN – Implementacja i Architektura SOLID)

Zaimplementuj metodę `evalRPN` w klasie `RPN` tak, aby realizowała całą logikę opisaną w specyfikacji powyżej.

### Wymagania architektoniczne (SOLID):

Projekt rozwiązania musi spełniać dobre praktyki programowania obiektowego, ze szczególnym uwzględnieniem zasad **SOLID**:

1. **Zasada Jednej Odpowiedzialności (Single Responsibility Principle – SRP):**
    - Podziel kod na mniejsze, spójne klasy/komponenty wydelegowane do konkretnych zadań, np.:
        - Parsowanie tokenów i rozpoznawanie systemów liczbowych.
        - Walidacja poprawności składniowej wyrażenia.
        - Wykonywanie samych operacji matematycznych.

    - Klasa `RPN` / metoda `evalRPN` powinna pełnić rolę orkiestratora procesu, a nie zawierać całą logikę w jednej wielkiej metodzie (`God Method`).


2. **Zasada Otwarte-Zamknięte (Open/Closed Principle – OCP):**
    - Architektura powinna być **otwarta na rozbudowę, ale zamknięta na modyfikacje**.
    - Dodanie nowego operatora (np. potęgowania `^`, modulu `%`) lub nowego systemu liczbowego (np. ósemkowego `O`) powinno odbywać się poprzez **dopisanie nowej klasy/klucza w rejestrze**, a **nie poprzez edycję instrukcji `switch` / `if-else**` w głównej pętli ewaluatora RPN (zastosuj np. wzorzec *Strategia*, *Słownik operatorów* lub polimorfizm).


**Kryterium sukcesu:** Kod jest uznany za ukończony, gdy architektura spełnia powyższe zasady SOLID, a wszystkie testy jednostkowe napisane w **Zadaniu 1 (Faza RED)** przechodzą pomyślnie (status **GREEN**).

> **Uwaga:** [Zasady SOLID](https://www.samouczekprogramisty.pl/solid-czyli-dobre-praktyki-w-programowaniu-obiektowym/).
