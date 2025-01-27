## Historie
1. Jako użytkownik, chcę szybko wybrać rodzaj biletu, aby zminimalizować czas
spędzony przy biletomacie.
2. Jako użytkownik, chcę mieć możliwość wyboru języka, aby móc korzystać z
biletomatu bez względu na znajomość języka lokalnego.
3. Jako użytkownik, chcę sprawdzić poprawność transakcji przed jej finalizacją,
aby uniknąć pomyłek.
4. Jako użytkownik, chcę otrzymać potwierdzenie zakupu (np. wydruk biletu lub
elektroniczny bilet), aby móc korzystać z transportu zgodnie z przepisami
5. Jako użytkownik, chcę płacić za bilet kartą, gotówką lub telefonem, aby mieć
większą elastyczność w wyborze metody płatności.
6. Jako użytkownik, chcę otrzymać wyraźne instrukcje na ekranie, aby wiedzieć,
jak dokonać zakupu krok po kroku.
7. Jako użytkownik, chcę widzieć czas pozostały na decyzję (np. wyświetlany
licznik czasu), aby móc szybko podjąć działanie.



## Płatność za bilet
```mermaid
flowchart TD
    U[Użytkownik]
    S[Biletomat]

    %% Główny przepływ
    U --> MP[Wybór metody płatności]
    MP --> VP[Weryfikacja metody płatności]
    VP --> RP[Realizacja płatności]
    RP --> PT[Potwierdzenie transakcji]

    %% Relacje Include
    MP -.->|«include»| VP2[Weryfikacja płatności]
    RP -.->|«include»| CANCEL[Anulowanie transakcji]

    %% Relacja Extend
    %% "Obsługa błędów płatności" rozszerza przypadki związane z wyborem płatności
    ERR[Obsługa błędów płatności]
    ERR -.->|«extend»| MP
    ERR -.->|«extend»| RP

    %% Użytkownik może anulować proces w dowolnym momencie
    U --- CANCEL
```
## Otrzymanie instrukcji na ekranie
```mermaid
flowchart TD
    U[Użytkownik]
    S[Biletomat]

    %% Główny przepływ
    U --> RI[Rozpoczęcie interakcji]
    RI --> WI[Wyświetlenie instrukcji]
    WI --> PI[Postępowanie według instrukcji]
    PI --> HELP[Wyświetlenie pomocy]

    %% Relacje Include
    PI -.->|«include»| CANCEL[Anulowanie transakcji]

    %% Asocjacja anulowania – użytkownik może przerwać proces w dowolnym momencie
    U --- CANCEL
```
