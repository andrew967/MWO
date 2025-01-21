## Historie
1. Jako biletomat, chcę automatycznie aktualizować listę dostępnych biletów i ich
cen, aby zapewnić zgodność z polityką przewoźnika.
2. Jako biletomat, chcę rejestrować wszystkie transakcje i wysyłać raporty do
systemu centralnego, aby umożliwić monitoring i kontrolę operacji.
3. Jako biletomat, chcę posiadać czytelny ekran dotykowy, aby użytkownik mógł
łatwo nawigować po interfejsie.
4. Jako biletomat, chcę być wyposażony w różne metody płatności (terminal kart,
czytnik gotówki, NFC), aby obsługiwać różnorodne transakcje.
5. Jako biletomat, chcę wydawać resztę w gotówce, jeśli użytkownik zapłaci
nadmiarowo, aby transakcja była zgodna z oczekiwaniami.

## Wyświetlenie podsumowania transakcji
```mermaid
flowchart TD
    system[Biletomat]
    U[Użytkownik]
    
    %% Główne przypadki użycia
    A[Gromadzenie danych o transakcji]
    C[Wyświetlenie podsumowania]
    D[Oczekiwanie na decyzję użytkownika]
    
    %% Relacja Include (przerywana linia)
    E[Podsumowanie transakcji]
    
    %% Relacja Extend – skierowana od "Obsługa anulowania" do "Oczekiwanie na decyzję użytkownika" (przerywana linia)
    F[Obsługa anulowania] -.->|«extend»| D
    
    %% Połączenia głównego przepływu
    system --> A
    A --> C
    C --> D
    U --- D 
    
    %% Relacja Include (przerywana linia)
    C -.->|«include»| E

```
## Generowanie potwierdzenia zakupu
```mermaid
flowchart TD
    BT[Biletomat]
    
    %% Główny przepływ
    BT --> A[Odbiór potwierdzenia zakończenia transakcji]
    A --> B[Generowanie potwierdzenia zakupu]
    B --> C[Informacja o potwierdzeniu]
    C --> D[Oczekiwanie na odbiór przez użytkownika]

    %% Relacja Include
    B -.->|«include»| GB[Generowanie biletu]
    
    %% Relacja Extend – od "Powiadomienie o błędzie generowania potwierdzenia" do "Generowanie potwierdzenia zakupu"
    ERR[Błąd generowania] -.->|«extend»| B

```
