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
### Wyświetlenie dostępnych biletów + Obsługa wyboru języka + Wyświetlenie podsumowania transakcji
```mermaid
flowchart TD
    U((Użytkownik))
    B((Biletomat))
    
    %% Ekran powitalny i wyświetlenie biletów
    A1[Uruchomienie ekranu powitalnego]
    A2[Pobranie listy biletów]
    A3[Wyświetlenie biletów]
    A4[Oczekiwanie na wybór użytkownika]
    A5[Aktualizacja biletów]
    A6[Ostrzeżenie o braku danych]
    
    %% Wybór języka
    L1[Wyświetlenie opcji językowych]
    L2[Rejestracja wyboru języka]
    L3[Dostosowanie interfejsu]
    L4[Opcje językowe]
    L5[Powrót do języka domyślnego]
    
    %% Podsumowanie transakcji
    T1[Gromadzenie danych o transakcji]
    T2[Wyświetlenie podsumowania]
    T3[Oczekiwanie na decyzję użytkownika]
    T4[Podsumowanie transakcji]
    T5[Obsługa anulowania]
    
    %% Główny przepływ - ekran powitalny
    B --> A1
    A1 --> A2
    A2 --> A3
    A3 --> A4
    A2 -->|Include| A5
    A2 -->|Extend| A6
    
    %% Główny przepływ - wybór języka
    B --> L1
    L1 --> L2
    L2 --> L3
    L1 -->|Include| L4
    L3 -->|Extend| L5
    
    %% Główny przepływ - podsumowanie
    A4 --> T1
    T1 --> T2
    T2 --> T3
    T2 -->|Include| T4
    T3 -->|Extend| T5
    
    %% Interakcje użytkownika
    U --> A4
    U --> L2
    U --> T3
```
