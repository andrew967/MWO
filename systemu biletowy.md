## Historie
1. Jako system biletowy, chcę dostarczać aktualne dane o taryfach i typach
biletów do biletomatu, aby użytkownik miał zawsze poprawne informacje.
2. Jako system biletowy, chcę umożliwiać sprawdzenie ważności biletu w czasie
rzeczywistym, aby zapobiegać oszustwom.
3. Jako system biletowy, chcę rejestrować każde sprzedane bilety, aby śledzić
ruch i sprzedaż w systemie.
4. Jako system biletowy, chcę współpracować z aplikacjami mobilnymi, aby
użytkownik mógł uzyskać elektroniczny bilet w przypadku takiego wyboru.

## DIAGRAMY PRZYPADKÓW UŻYCIA
### Dostarczanie listy biletów do biletomatu
```mermaid
flowchart TD
    Biletomat --> OdebranieZadaniaListy[Odebranie żądania listy biletów]
    OdebranieZadaniaListy --> SprawdzenieTaryf[Sprawdzenie bazy taryf]
    SprawdzenieTaryf --> PrzeslanieListy[Przesłanie listy biletów]

    %% Relacje Include
    OdebranieZadaniaListy -->|Include| SprawdzenieTaryf

    %% Relacje Extend
    PrzeslanieListy -->|Extend| BladKomunikacji[Błąd komunikacji]
```
