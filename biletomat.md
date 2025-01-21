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

## Diagramy przypadków użycia 

### Obsługa wyboru języka

```mermaid
flowchart TD
  U[Biletomat] --> A[Wyświetlenie opcji językowych]
  A --> B[Rejestracja wyboru języka]  
  B --> C[Dostosowanie interfejsu]
  
  A -.->|«include»| D[Opcje językowe]
  
  E[Powrót do języka domyślnego] -.->|«extend»| C
```

### Wyświetlenie dostępnych biletów

```mermaid
flowchart TD  
    U[Użytkownik] --> A[Uruchomienie ekranu powitalnego]  
    A --> B[Pobranie listy biletów]  
    B --> C[Wyświetlenie biletów]  
    C --> D[Oczekiwanie na wybór użytkownika]  

    B -.->|«include»| E[Aktualizacja biletów]  

    F[Ostrzeżenie o braku danych] -.->|«extend»| B
```
### Wyświetlenie podsumowania transakcji
```mermaid
flowchart TD
    system[Biletomat]
    U[Użytkownik]
    
    
    A[Gromadzenie danych o transakcji]
    C[Wyświetlenie podsumowania]
    D[Oczekiwanie na decyzję użytkownika]
    
    
    E[Podsumowanie transakcji]
    
  
    F[Obsługa anulowania] -.->|«extend»| D
    
    
    system --> A
    A --> C
    C --> D
    U --- D 
  
    C -.->|«include»| E

```
## Generowanie potwierdzenia zakupu
```mermaid
flowchart TD
    BT[Biletomat]
    
    
    BT --> A[Odbiór potwierdzenia zakończenia transakcji]
    A --> B[Generowanie potwierdzenia zakupu]
    B --> C[Informacja o potwierdzeniu]
    C --> D[Oczekiwanie na odbiór przez użytkownika]

   
    B -.->|«include»| GB[Generowanie biletu]
    
    
    ERR[Błąd generowania] -.->|«extend»| B


```
