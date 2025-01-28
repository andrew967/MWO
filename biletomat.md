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
### Generowanie potwierdzenia zakupu
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
### Realizacja płatności
```mermaid
flowchart TD
    BT[Biletomat]
    
    %% Główny przepływ
    BT --> A[Inicjowanie płatności]
    A --> B[Przesłanie danych transakcji]
    B --> C[Oczekiwanie na odpowiedź systemu transakcyjnego]
    C --> D[Potwierdzenie płatności]

    %% Relacje Include
    A -.->|«include»| ERRP[Błędy płatności]
    B -.->|«include»| CANCEL[Anulowanie transakcji przez użytkownika]
    
    %% Relacja Extend – od "Obsługa alternatywnych metod płatności" do "Oczekiwanie na odpowiedź"
    ALT[Obsługa alternatyw] -.->|«extend»| C
```
### Wyświetlanie instrukcji
```mermaid
flowchart TD
    BT[Biletomat]
    
    %% Główny przepływ
    BT --> A[Wyświetlenie krokowych instrukcji]
    A --> B[Dostosowanie instrukcji w czasie rzeczywistym]
    B --> C[Wyświetlenie komunikatów pomocniczych]

    %% Relacje Include
    A -.->|«include»| BASIC[Podstawowe instrukcje]
    C -.->|«include»| CANCEL[Anulowanie transakcji przez użytkownika]

    %% Relacja Extend – od "Wyświetlenie szczegółowej pomocy (opcjonalnie)" do "Wyświetlenie komunikatów pomocniczych"
    EXT[Szczegółowa pomoc] -.->|«extend»| C
```
## Diagramy sekwencyj
### Obsługa wyboru języka
#### Scenariusz Główny (Podstawowy)

Cel: Biletomat wyświetla dostępne opcje językowe, odbiera wybór użytkownika i dostosowuje interfejs do wybranego języka.

Kroki:

- Wyświetlenie opcji języka:
    - Biletomat po uruchomieniu interakcji automatycznie prezentuje użytkownikowi ekran z dostępnymi opcjami językowymi.
    - Ekran zawiera listę dostępnych języków, a także opcję ustawienia języka domyślnego (operacja include).

- Odbiór wyboru języka:
    - Biletomat oczekuje na wybór użytkownika.
    - Po otrzymaniu wyboru, system przetwarza tę informację i automatycznie dostosowuje interfejs do wybranego języka.

- Dostosowanie interfejsu:
    - Po ustaleniu wyboru, Biletomat wykonuje procedurę zmiany interfejsu użytkownika.
    - Jeżeli użytkownik nie dokonał aktywnego wyboru, system może automatycznie ustawić język domyślny (include).

- Zakończenie podstawowego przepływu:
    - Interfejs zostaje dostosowany do wybranego (lub domyślnego) języka, a użytkownik kontynuuje dalsze interakcje.

#### Scenariusz Alternatywny

Cel: Umożliwić użytkownikowi uzyskanie dodatkowej listy popularnych języków oraz umożliwić anulowanie procesu wyboru języka.

Kroki:

- Rozszerzenie opcji wyboru języka:
    - Po wysłaniu przez Biletomat standardowej listy opcji językowych (krok 1 scenariusza głównego), użytkownik wysyła dodatkowe żądanie o wyświetlenie listy popularnych języków.
    - Biletomat, zgodnie z relacją extend, wykonuje operację wyświetlenia rozszerzonej listy popularnych języków.
    - Użytkownik przegląda rozszerzoną listę i dokonuje wyboru jednego z dostępnych języków, co skutkuje powrotem do głównego przepływu (krok 2 i 3 scenariusza głównego).

- Anulowanie procesu:
    - W dowolnym momencie interakcji (zarówno w głównym przepływie, jak i w alternatywnym scenariuszu) użytkownik może zdecydować o anulowaniu transakcji.
    - Po otrzymaniu sygnału anulowania, Biletomat przerywa proces wyboru języka i wysyła potwierdzenie anulowania.
    - Proces zostaje zakończony – system może powrócić do ekranu powitalnego lub zakończyć bieżącą sesję interakcji.
    
```mermaid
sequenceDiagram
    autonumber
    participant BT as Biletomat
    participant U as Użytkownik

    %% Biletomat rozpoczyna – wyświetla opcje językowe
    BT->>U: Wyświetlenie opcji języka

    %% Oczekiwanie na wybór dokonywany przez użytkownika
    U->>BT: Wybór języka
    BT->>U: Dostosowanie interfejsu do wybranego języka

    %% (Include) W przypadku, gdy nie określono wyboru, domyślny język może być ustawiony
    BT->>U: (Include: Ustawienie domyślnego języka)

    %% Scenariusz rozszerzający – użytkownik żąda alternatywnych opcji
    U->>BT: Żądanie listy popularnych języków
    BT->>U: (Extend: Wyświetlenie listy popularnych języków)

    %% Możliwość anulowania procesu przez użytkownika
    U->>BT: Anulowanie transakcji
    BT->>U: Potwierdzenie anulowania
```

### Wyświetlanie instrukcji

#### AKTOR: Biletomat.
#### OBIEKTY: Użytkownik.
#### SCENARUISZ GŁOWNY:
	•	Biletomat wyświetla krokowe instrukcje użytkownikowi na ekranie.
	•	Biletomat monitoruje aktywność użytkownika.
#### SCENARIUSZ ALTERNATYWNY 1 (Brak aktywności lub błąd):
	•	Biletomat wykrywa brak aktywności użytkownika.
	•	Wyświetla komunikat pomocniczy, informujący o konieczności podjęcia działań.
	•	Jeśli problem się utrzymuje, biletomat oferuje szczegółową pomoc w formie dodatkowych instrukcji.

#### SCENARIUSZ ALTERNATYWNY 2 (Anulowanie transakcji):
	•	Użytkownik wybiera opcję anulowania transakcji.
	•	Biletomat wyświetla potwierdzenie anulowania i kończy operację.

```mermaid
sequenceDiagram
    participant USER as Użytkownik
    participant MACHINE as Biletomat

    MACHINE->>USER: Wyświetlenie krokowych instrukcji
    loop Monitorowanie aktywności
        MACHINE->>MACHINE: Analiza aktywności użytkownika
        alt Użytkownik aktywny
            MACHINE->>USER: Aktualizacja instrukcji
        else Brak aktywności lub błąd
            MACHINE->>USER: Wyświetlenie komunikatu pomocniczego
            opt Szczegółowa pomoc
                MACHINE->>USER: Wyświetlenie szczegółowych instrukcji
            end
        end
    end
    opt Anulowanie przez użytkownika
        USER->>MACHINE: Anulowanie transakcji
        MACHINE->>USER: Komunikat o anulowaniu
    end

```


### Wyświetlenie dostępnych biletów

#### AKTOR: Użytkownik
#### OBIEKTY: Biletomat, System Centralny
#### Kolejność komunikatów (Scenariusz Główny):
	- Biletomat uruchamia ekran powitalny (Uruchomienie ekranu powitalnego).
	- Biletomat pobiera listę dostępnych biletów z systemu centralnego (include: Aktualizacja biletów).
	- Biletomat wyświetla kategorię biletów i ich szczegóły (Wyświetlenie biletów).
	- Biletomat czeka na wybór użytkownika (Oczekiwanie na wybór użytkownika).
#### Scenariusz Alternatywny (Ostrzeżenie o braku danych):
	- Podczas próby pobrania listy dostępnych biletów (krok 2 scenariusza głównego) występuje błąd (np. awaria sieci).
	- Zgodnie z relacją extend, Biletomat wyświetla ostrzeżenie o braku aktualnych danych.
	- Użytkownik może spróbować ponownie lub zrezygnować z zakupu, co powoduje powrót do ekranu powitalnego lub zakończenie sesji.

```mermaid
sequenceDiagram
    autonumber
    participant U as Użytkownik
    participant BT as Biletomat
    participant SC as System Centralny

    %% Krok 1: Uruchomienie ekranu powitalnego
    BT->>U: Ekran powitalny (start)

    %% Krok 2: Pobranie listy dostępnych biletów (include: Aktualizacja biletów)
    BT->>SC: Żądanie listy dostępnych biletów
    alt Dostęp do systemu centralnego OK
        SC-->>BT: Lista dostępnych biletów
    else Awaria sieci (extend: Ostrzeżenie o braku danych)
        BT->>U: Komunikat o braku aktualnych danych
        note right of BT: Użytkownik może ponowić próbę <br/> lub zakończyć sesję
    end

    %% Krok 3: Wyświetlenie biletów
    BT->>U: Wyświetlenie kategorii i szczegółów biletów

    %% Krok 4: Oczekiwanie na wybór użytkownika
    U->>BT: Wybór biletu lub rezygnacja

    %% Zakończenie
    BT->>U: Przejście do dalszej części zakupu <br/> lub powrót do ekranu głównego

```

## Diagramy klas
### Wyświetlanie instrukcji
## OPIS KLAS

### KLASY

#### BILETOMAT
- **Atrybuty:** brak
- **Metody:**
  - `void wyswietlInstrukcje()` – Wyświetla krokowe instrukcje dla użytkownika.
  - `void monitorujAktywnosc()` – Monitoruje aktywność użytkownika.
  - `void dostosujInstrukcje()` – Dostosowuje wyświetlane instrukcje w czasie rzeczywistym.
  - `void wyswietlKomunikatyPomocnicze()` – Wyświetla komunikaty pomocnicze w przypadku błędów użytkownika.
  - `void anulujTransakcje()` – Anuluje trwającą transakcję.

#### INSTRUKCJA
- **Atrybuty:**
  - `String tresc` – Treść instrukcji.
  - `String typ` – Typ instrukcji (np. podstawowa, szczegółowa).
- **Metody:**
  - `void wyswietl()` – Wyświetla instrukcję.

#### UZYTKOWNIK
- **Atrybuty:**
  - `boolean aktywnosc` – Status aktywności użytkownika.
- **Metody:**
  - `void interakcja()` – Rejestruje interakcję użytkownika z biletomatem.
  - `void anulujTransakcje()` – Pozwala użytkownikowi anulować transakcję.

#### PODSTAWOWEINSTRUKCJE
- **Metody:**
  - `void wyswietlPodstawoweInstrukcje()` – Wyświetla podstawowe instrukcje krokowe.

#### SZCZEGOLOWAPOMOC
- **Metody:**
  - `void wyswietlSzczegolowaPomoc()` – Wyświetla szczegółowe instrukcje, gdy użytkownik napotka problemy.

#### ANULOWANIETRANSAKCJI
- **Metody:**
  - `void wykonajAnulowanie()` – Wykonuje anulowanie transakcji.

---

### RELACJE:
- `BILETOMAT` jest powiązany z `INSTRUKCJA` – Wyświetla instrukcje użytkownikowi.
- `BILETOMAT` monitoruje aktywność `UZYTKOWNIK`.
- `BILETOMAT` korzysta z `PODSTAWOWEINSTRUKCJE` poprzez relację `<<include>>`.
- `BILETOMAT` wywołuje `SZCZEGOLOWAPOMOC` w sytuacjach wyjątkowych poprzez relację `<<extend>>`.
- `BILETOMAT` korzysta z `ANULOWANIETRANSAKCJI` w przypadku anulowania operacji przez użytkownika (`<<include>>`).
  
```mermaid
classDiagram
class BILETOMAT {
  + void wyswietlInstrukcje()
  + void monitorujAktywnosc()
  + void dostosujInstrukcje()
  + void wyswietlKomunikatyPomocnicze()
  + void anulujTransakcje()
}
class INSTRUKCJA {
  - String tresc
  - String typ
  + void wyswietl()
}
class UZYTKOWNIK {
  - boolean aktywnosc
  + void interakcja()
  + void anulujTransakcje()
}
class PODSTAWOWEINSTRUKCJE {
  + void wyswietlPodstawoweInstrukcje()
}
class SZCZEGOLOWAPOMOC {
  + void wyswietlSzczegolowaPomoc()
}
class ANULOWANIETRANSAKCJI {
  + void wykonajAnulowanie()
}

BILETOMAT --> INSTRUKCJA : wyswietla
BILETOMAT --> UZYTKOWNIK : monitoruje
BILETOMAT --> PODSTAWOWEINSTRUKCJE : <<include>>
BILETOMAT --> SZCZEGOLOWAPOMOC : <<extend>>
BILETOMAT --> ANULOWANIETRANSAKCJI : <<include>>


```
## OPIS KLAS

### KLASY
#### BILETOMAT
- **ATRYBUTY:** 
  - `STRING ID_BILETOMATU`
  - `BOOLEAN CZY_DOSTEPNY`
  - `LIST<BILET> LISTA_BILETOW`
- **METODY:**
  - `VOID URUCHOM_EKRAN()`
  - `LIST<BILET> POBIERZ_LISTE_BILETOW()`
  - `VOID WYSWIETL_BILETY()`
  - `VOID WYSWIETL_KOMUNIKAT_O_BLEDZIE()`

#### SYSTEM CENTRALNY
- **ATRYBUTY:** 
  - `LIST<BILET> DOSTEPNE_BILETY`
- **METODY:**
  - `LIST<BILET> ZWROC_DOSTEPNE_BILETY()`

#### BILET
- **ATRYBUTY:** 
  - `STRING NAZWA`
  - `DOUBLE CENA`
  - `STRING KATEGORIA`
- **METODY:**
  - `STRING POBIERZ_OPIS()`

#### UZYTKOWNIK
- **ATRYBUTY:** 
  - `STRING ID_UZYTKOWNIKA`
  - `STRING WYBRANY_BILET`
- **METODY:**
  - `VOID WYBIERZ_BILET(STRING BILET)`

### RELACJE
- `BILETOMAT` jest połączony z `SYSTEM CENTRALNY` poprzez pobieranie listy dostępnych biletów (asocjacja).
- `BILETOMAT` wyświetla informacje o `BILET` (kompozycja).
- `UZYTKOWNIK` komunikuje się z `BILETOMAT` poprzez wybór biletu (asocjacja).

### WIZUALIZACJA DIAGRAMU KLAS
```mermaid
classDiagram

class Biletomat {
  - STRING ID_BILETOMATU
  - BOOLEAN CZY_DOSTEPNY
  - LIST<BILET> LISTA_BILETOW
  + VOID URUCHOM_EKRAN()
  + LIST<BILET> POBIERZ_LISTE_BILETOW()
  + VOID WYSWIETL_BILETY()
  + VOID WYSWIETL_KOMUNIKAT_O_BLEDZIE()
}

class SystemCentralny {
  - LIST<BILET> DOSTEPNE_BILETY
  + LIST<BILET> ZWROC_DOSTEPNE_BILETY()
}

class Bilet {
  - STRING NAZWA
  - DOUBLE CENA
  - STRING KATEGORIA
  + STRING POBIERZ_OPIS()
}

class Uzytkownik {
  - STRING ID_UZYTKOWNIKA
  - STRING WYBRANY_BILET
  + VOID WYBIERZ_BILET(STRING BILET)
}

Biletomat --> SystemCentralny : Pobiera dane
Biletomat o-- Bilet : Wyświetla szczegóły
Uzytkownik --> Biletomat : Wybiera bilet

```