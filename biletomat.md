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
### Wyświetlenie dostępnych biletów

```mermaid
flowchart TD  
    U[Użytkownik] --> A[Uruchomienie ekranu powitalnego]  
    A --> B[Pobranie listy biletów]  
    B --> C[Wyświetlenie biletów]  
    C --> D[Oczekiwanie na wybór użytkownika]  

    %% Relacje Include  
    B -->|Include| E[Aktualizacja biletów]  

    %% Relacje Extend  
    B -->|Extend| F[Ostrzeżenie o braku danych]  
```

### Obsługa wyboru języka

```mermaid

flowchart TD
  U[Biletomat] --> A[Wyświetlenie opcji językowych]
  A --> B[Rejestracja wyboru języka]  
  B --> C[Dostosowanie interfejsu]  
  A -->|Include| D[Opcje językowe]  
  C -->|Extend| E[Powrót do języka domyślnego]
```

### Wyświetlenie podsumowania transakcji
```mermaid
flowchart TD
    B((Biletomat))
    U((Użytkownik))
    
    %% Główne przypadki użycia
    A[Gromadzenie danych o transakcji]
    C[Wyświetlenie podsumowania]
    D[Oczekiwanie na decyzję użytkownika]
    
    %% Relacje Include
    E[Podsumowanie transakcji]
    
    %% Relacja Extend
    F[Obsługa anulowania]
    
    %% Połączenia głównego przepływu
    B --> A
    A --> C
    C --> D
    U --> D
    
    %% Relacje Include
    C -->|Include| E
    
    %% Relacja Extend
    D -->|Extend| F
    
```
### Wyświetlenie dostępnych biletów i Obsługa wyboru języka
```mermaid
flowchart TD  
     
 
```
