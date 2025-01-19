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


## DIAGRAMY PRZYPADKÓW UŻYCIA
### SZYBKI WYBÓR RODZAJU BILETU
```mermaid
flowchart TD
    U[Użytkownik] --> A[Rozpoczęcie interakcji]
    A --> B[Wybór kategorii]
    B --> C[Wybór biletu]
    C --> D[Wyświetlenie podsumowania]
    D --> E[Potwierdzenie wyboru]
    E --> F[Anulowanie transakcji]

    %% Relacje Include
    C -->|Include| G[Sprawdzenie biletów]
    E -->|Include| F

    %% Relacje Extend
    B -->|Extend| H[Podpowiedź interfejsu]
    C -->|Extend| H

```

### Wybór języka

```mermaid
flowchart TD  
    U[Użytkownik] --> A[Rozpoczęcie interakcji]  
    A --> B[Wyświetlenie opcji języka]  
    B --> C[Wybór języka]  
    C --> D[Dostosowanie interfejsu]  
    C --> F[Anulowanie transakcji]  

  
    C -->|Include| G[Domyślny język]  
    D -->|Include| F  

    B -->|Extend| H[Lista popularnych języków]
```

### Sprawdzenie poprawności transakcji
```mermaid
flowchart TD
    U((Użytkownik))
    
    %% Główne przypadki użycia
    A[Wybór biletu i płatności]
    B[Wyświetlenie podsumowania]
    C[Potwierdzenie lub cofnięcie]
    D[Kontynuacja lub anulowanie]
    
    %% Relacje Include
    E[Podsumowanie transakcji]
    F[Anulowanie transakcji]
    
    %% Relacja Extend
    G[Ostrzeżenie o błędzie]
    
    %% Połączenia głównego przepływu
    U --> A
    A --> B
    B --> C
    C --> D
    
    %% Relacje Include
    B -->|Include| E
    A & B & C & D -->|Include| F
    
    %% Relacja Extend
    A & B -->|Extend| G
    
    %% Stylizacja
    classDef default fill:#f9f9f9,stroke:#333,stroke-width:2px
    classDef actor fill:#e1f5fe,stroke:#0277bd,stroke-width:2px
    class U actor

```


