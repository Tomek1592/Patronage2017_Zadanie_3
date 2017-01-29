# Patronage 2017 - Zadanie 3 - Tomasz Wołoszyk

## Kurs Javascript na Codeacademy

Link do ukończonego kursu na Codeacademy: https://www.codecademy.com/Tomek1592

## Technologie

1. Vue.js
2. Bulma.css
3. Webpack-simple

## Licznik (Score)

Każdy nowo dodany licznik dostaje id o jeden większe od poprzednika. Jeżeli nie ma żadnego licznika, id licznika przyjmuje wartość 1.

## Widoki

### Main View
![alt text](main-view.PNG "Main View")

#### Opis widoku
1. Przycisk dodawania nowego licznika,
2. Usuwanie licznika,
3. Nazwa licznika,
4. Wartość licznika,
5. Zwiększanie wartości licznika o 1,
6. Zmniejszanie wartości licznika o 1,
7. Pole do wpisania nowej wartości licznika,
8. Wyświetlenie wartości licznika w modalu Get Alert Modal,
9. Zatwierdzenie nowej wartości licznika, pobranej z pola 7,
10. Resetowanie licznika do wartości 0 (w zależności od formatowania).

#### Funkcjonalności
- Kiedy wartość licznika wynosi 0, przycisk "-" i "reset" są nieaktywne,
- Kiedy wartość licznika jest maksymalna, przycisk "+" jest nieaktywny,
- Po wpisaniu wartości niecałkowitej, zostanie ona zaokrąglona w dół (np. 2,3 zostanie zapisana jako 2),
- Po naciśnięciu przycisku get, zostaje otwarty modal Get Modal,
- Po naciśnięciu litery 'X' w prawym górnym rogu licznika, zostaje on usunięty,
- Zmiana wartości licznika (Set) posiada pełną walidację.

### Add Counter Modal View - dodawanie nowego licznika
![alt text](add-counter-modal-view.PNG "Add Counter Modal")

#### Opis widoku
1. Zamknięcie okna,
2. Tytuł okna,
3. Pole do wpisania wartości formatu (1-4),
4. Pole do wpisania wartości licznika (w zależności od wybranej wartości formatu),
5. Dodanie nowego licznika.

#### Funkcjonalności
- Modal można zamknąć poprzez naciśnięcie litery 'X' w prawy górnym rogu, 
  bądź naciskając dowolne miejsce na przyciemnionym tle,
- Jeżeli format nie jest wypełniony, pole value i przycisk Add Counter są nieaktywne,
- Okno dodawania posiada pełną walidację.

### Get Value Modal View - wyświetlanie wartości konkretnego licznika
![alt text](get-value-modal-view.PNG "Get Value Modal")

#### Opis widoku
1. Zamknięcie okna, 
2. Tytuł wraz z numerem licznika, dla którego wyświetlamy wartość,
3. Wartość licznika.

#### Funkcjonalności
- Modal można zamknąć poprzez naciśnięcie litery 'X' w prawy górnym rogu, 
  bądź naciskając dowolne miejsce na przyciemnionym tle,

