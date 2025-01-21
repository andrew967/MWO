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

## Diagramy przypadków użycia 
### Wybór języka

```mermaid
flowchart TD  
    U[Użytkownik] --> A[Rozpoczęcie interakcji]  
    A --> B[Wyświetlenie opcji języka]  
    B --> C[Wybór języka]  
    C --> D[Dostosowanie interfejsu]  
    
    %% Relacja Include (przerywana linia)
    C -.->|«include»| G[Domyślny język]
    
    %% Relacja Extend – odwrócona: "Lista popularnych języków" wskazuje na "Wyświetlenie opcji języka"
    H[Lista popularnych języków] -.->|«extend»| B

    %% Umożliwienie anulowania na każdym etapie - dodałem asocjację z procesem
    CANCEL[Anulowanie transakcji]
    U --- CANCEL
    C --- CANCEL
    D --- CANCEL
```

### Szybki wybór rodzaju biletu
```mermaid
flowchart TD
    U[Użytkownik] --> A[Rozpoczęcie interakcji]
    A --> B[Wybór kategorii]
    B --> C[Wybór biletu]
    C --> D[Wyświetlenie podsumowania]
    D --> E[Potwierdzenie wyboru]
    E --> I[Anulowanie transakcji]

    %% Relacje Include (przerywane linie)
    C -.->|«include»| G[Sprawdzenie biletów]
    %% Alternatywnie – dodajemy możliwość anulowania przez include z "Potwierdzenie wyboru"
    E -.->|«include»| I

    %% Relacje Extend (przerywane linie, odwrotne relacje)
    H1[Podpowiedź interfejsu] -.->|«extend»| B
    H2[Podpowiedź interfejsu] -.->|«extend»| C

    %% Użytkownik ma możliwość anulowania na każdym etapie – asocjacja
    U --- I
```
