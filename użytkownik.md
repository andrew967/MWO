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

## SPRAWDZENIE POPRAWNOŚCI TRANSAKCJI
```mermaid
flowchart TD
    U[Użytkownik]
    
    %% Główne przypadki użycia
    A[Wybór biletu i płatności]
    B[Wyświetlenie podsumowania]
    C[Potwierdzenie lub cofnięcie]
    D[Kontynuacja lub anulowanie]
    
    %% Relacje Include (przerywane linie)
    B -.->|«include»| E[Podsumowanie transakcji]
    A -.->|«include»| F[Anulowanie transakcji]
    B -.->|«include»| F
    C -.->|«include»| F
    D -.->|«include»| F
    
    %% Relacja Extend – odwrócona:
    %% "Ostrzeżenie o błędzie" wskazuje na "Wybór biletu i płatności" oraz "Wyświetlenie podsumowania"
    G[Ostrzeżenie o błędzie] -.->|«extend»| A
    G -.->|«extend»| B

    %% Połączenia głównego przepływu
    U --> A
    A --> B
    B --> C
    C --> D

    %% Umożliwienie anulowania przez użytkownika w dowolnej chwili
    U --- F
```

## Otrzymanie potwierdzenia zakupu
```mermaid
flowchart TD
    U[Użytkownik]
    S[Biletomat]

    %% Główny przepływ
    S --> A[Generowanie potwierdzenia]
    A --> B[Odebranie potwierdzenia]
    B --> C[Komunikat o zakończeniu]

    %% Relacje Include
    A -.->|«include»| GT[Generowanie biletu]
    B -.->|«include»| CANCEL[Anulowanie transakcji]

    %% Relacja Extend
    %% Relacja od "Wybór formy potwierdzenia" wskazuje na "Generowanie potwierdzenia"
    WF[Wybór formy potwierdzenia]
    WF -.->|«extend»| A

    %% Użytkownik może anulować w dowolnym momencie
    U --- CANCEL

```
