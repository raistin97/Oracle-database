-- Created by Vertabelo (http://vertabelo.com)
-- Last modification date: 2021-01-05 15:38:58.015

-- foreign keys
ALTER TABLE Dania
    DROP CONSTRAINT Dania_Kuchnia;

ALTER TABLE Dania
    DROP CONSTRAINT Dania_Menu_Dnia;

ALTER TABLE Menu_Dnia
    DROP CONSTRAINT Menu_Dnia_Sala;

ALTER TABLE Pracowni_Sali
    DROP CONSTRAINT Pracowni_Sali_Pracownik;

ALTER TABLE Pracowni_Sali
    DROP CONSTRAINT Pracowni_Sali_Sala;

ALTER TABLE Pracownik_kuchni
    DROP CONSTRAINT Pracownik_kuchni_Kuchnia;

ALTER TABLE Pracownik_kuchni
    DROP CONSTRAINT Pracownik_kuchni_Pracownik;

ALTER TABLE Rezerwacja
    DROP CONSTRAINT Rezerwacja_klient;

ALTER TABLE Specyfikacje
    DROP CONSTRAINT Specyfikacje_Dania;

ALTER TABLE Specyfikacje
    DROP CONSTRAINT Table_11_Rezerwacja;

-- tables
DROP TABLE Dania;

DROP TABLE Kuchnia;

DROP TABLE Menu_Dnia;

DROP TABLE Pracowni_Sali;

DROP TABLE Pracownik;

DROP TABLE Pracownik_kuchni;

DROP TABLE Rezerwacja;

DROP TABLE Sala;

DROP TABLE Specyfikacje;

DROP TABLE klient;

-- End of file.








-- Created by Vertabelo (http://vertabelo.com)
-- Last modification date: 2021-01-05 15:38:58.015

-- tables
-- Table: Dania
CREATE TABLE Dania (
    ID_dania integer  NOT NULL,
    Rodzaj_dania varchar2(30)  NOT NULL,
    ID_Kuchni integer  NOT NULL,
    Dnia_Ilosc_Dan integer  NOT NULL,
    CenaZaDanie integer NOT NULL,
    CONSTRAINT Dania_pk PRIMARY KEY (ID_dania)
) ;

-- Table: Kuchnia
CREATE TABLE Kuchnia (
    Ilosc_Pracownikow integer  NOT NULL,
    Rodzaj_Dan varchar2(40)  NOT NULL,
    ID_Kuchni integer  NOT NULL,
    CONSTRAINT Kuchnia_pk PRIMARY KEY (ID_Kuchni)
) ;

-- Table: Menu_Dnia
CREATE TABLE Menu_Dnia (
    Ilosc_Dan integer  NOT NULL,
    Dania varchar2(40)  NOT NULL,
    ID_Sali integer  NOT NULL,
    CONSTRAINT Menu_Dnia_pk PRIMARY KEY (Ilosc_Dan)
) ;

-- Table: Pracowni_Sali
CREATE TABLE Pracowni_Sali (
    ID_PracownikaSali integer  NOT NULL,
    Id_Pracownika integer  NOT NULL,
    ID_Sali integer  NOT NULL,
    Stanowisko varchar2(30)  NOT NULL,
    Zmiana_koniec integer  NOT NULL,
    Zmiana_poczatek integer  NOT NULL,
    CONSTRAINT Pracowni_Sali_pk PRIMARY KEY (ID_PracownikaSali)
) ;

-- Table: Pracownik
CREATE TABLE Pracownik (
    Id_Pracownika integer  NOT NULL,
    Imie varchar2(30)  NOT NULL,
    Nazwisko varchar2(30)  NOT NULL,
    Zarobki integer  NOT NULL,
    CONSTRAINT Pracownik_pk PRIMARY KEY (Id_Pracownika)
) ;

-- Table: Pracownik_kuchni
CREATE TABLE Pracownik_kuchni (
    ID_PracownikaKuchni integer  NOT NULL,
    Id_Pracownika integer  NOT NULL,
    ID_Kuchni integer  NOT NULL,
    Stanowisko varchar2(30)  NOT NULL,
    zmiana_koniec integer  NOT NULL,
    zmiana_poczatek integer  NOT NULL,
    CONSTRAINT Pracownik_kuchni_pk PRIMARY KEY (ID_PracownikaKuchni)
) ;

-- Table: Rezerwacja
CREATE TABLE Rezerwacja (
    ID_Rezerwacji integer  NOT NULL,
    Ilosc_osob integer  NOT NULL,
    data timestamp  NOT NULL,
    ID_Klienta integer  NOT NULL,
    CONSTRAINT Rezerwacja_pk PRIMARY KEY (ID_Rezerwacji)
) ;

-- Table: Sala
CREATE TABLE Sala (
    ID_Sali integer  NOT NULL,
    Ilosc_miejsc integer  NOT NULL,
    Ilosc_stolikow integer  NOT NULL,
    CONSTRAINT Sala_pk PRIMARY KEY (ID_Sali)
) ;

-- Table: Specyfikacje
CREATE TABLE Specyfikacje (
    ID_Rezerwacji integer  NOT NULL,
    ID_Specyfikacji integer  NOT NULL,
    ID_dania integer  NOT NULL,
    LACZNA_CENA integer NOT NULL,
    CONSTRAINT Specyfikacje_pk PRIMARY KEY (ID_Specyfikacji)
) ;

-- Table: klient
CREATE TABLE klient (
    ID_Klienta integer  NOT NULL,
    Imie varchar2(30)  NOT NULL,
    Nazwisko varchar2(30)  NOT NULL,
    CONSTRAINT klient_pk PRIMARY KEY (ID_Klienta)
) ;

-- foreign keys
-- Reference: Dania_Kuchnia (table: Dania)
ALTER TABLE Dania ADD CONSTRAINT Dania_Kuchnia
    FOREIGN KEY (ID_Kuchni)
    REFERENCES Kuchnia (ID_Kuchni);

-- Reference: Dania_Menu_Dnia (table: Dania)
ALTER TABLE Dania ADD CONSTRAINT Dania_Menu_Dnia
    FOREIGN KEY (Dnia_Ilosc_Dan)
    REFERENCES Menu_Dnia (Ilosc_Dan);

-- Reference: Menu_Dnia_Sala (table: Menu_Dnia)
ALTER TABLE Menu_Dnia ADD CONSTRAINT Menu_Dnia_Sala
    FOREIGN KEY (ID_Sali)
    REFERENCES Sala (ID_Sali);

-- Reference: Pracowni_Sali_Pracownik (table: Pracowni_Sali)
ALTER TABLE Pracowni_Sali ADD CONSTRAINT Pracowni_Sali_Pracownik
    FOREIGN KEY (Id_Pracownika)
    REFERENCES Pracownik (Id_Pracownika);

-- Reference: Pracowni_Sali_Sala (table: Pracowni_Sali)
ALTER TABLE Pracowni_Sali ADD CONSTRAINT Pracowni_Sali_Sala
    FOREIGN KEY (ID_Sali)
    REFERENCES Sala (ID_Sali);

-- Reference: Pracownik_kuchni_Kuchnia (table: Pracownik_kuchni)
ALTER TABLE Pracownik_kuchni ADD CONSTRAINT Pracownik_kuchni_Kuchnia
    FOREIGN KEY (ID_Kuchni)
    REFERENCES Kuchnia (ID_Kuchni);

-- Reference: Pracownik_kuchni_Pracownik (table: Pracownik_kuchni)
ALTER TABLE Pracownik_kuchni ADD CONSTRAINT Pracownik_kuchni_Pracownik
    FOREIGN KEY (Id_Pracownika)
    REFERENCES Pracownik (Id_Pracownika);

-- Reference: Rezerwacja_klient (table: Rezerwacja)
ALTER TABLE Rezerwacja ADD CONSTRAINT Rezerwacja_klient
    FOREIGN KEY (ID_Klienta)
    REFERENCES klient (ID_Klienta);

-- Reference: Specyfikacje_Dania (table: Specyfikacje)
ALTER TABLE Specyfikacje ADD CONSTRAINT Specyfikacje_Dania
    FOREIGN KEY (ID_dania)
    REFERENCES Dania (ID_dania);

-- Reference: Table_11_Rezerwacja (table: Specyfikacje)
ALTER TABLE Specyfikacje ADD CONSTRAINT Table_11_Rezerwacja
    FOREIGN KEY (ID_Rezerwacji)
    REFERENCES Rezerwacja (ID_Rezerwacji);

-- End of file.


INSERT INTO Pracownik(Id_Pracownika, Imie, Nazwisko, Zarobki)
VALUES (1, 'Robert', 'Lewandowski', 2200);
INSERT INTO PRACOWNIK(ID_PRACOWNIKA, IMIE, NAZWISKO, Zarobki)
VALUES (2, 'Jan', 'Kolonko', 3000);
INSERT INTO PRACOWNIK(ID_PRACOWNIKA, IMIE, NAZWISKO, Zarobki)
VALUES (3, 'Michal', 'Szpak', 2200);
INSERT INTO PRACOWNIK(ID_PRACOWNIKA, IMIE, NAZWISKO, Zarobki)
VALUES (4, 'Konrad', 'Makapaka', 6000);
INSERT INTO PRACOWNIK(ID_PRACOWNIKA, IMIE, NAZWISKO, Zarobki)
VALUES (5, 'Przemyslaw', 'Maciejewski', 5000);
INSERT INTO PRACOWNIK(ID_PRACOWNIKA, IMIE, NAZWISKO, Zarobki)
VALUES (6, 'Agnieszka', 'Imanowska', 5500);
INSERT INTO PRACOWNIK(ID_PRACOWNIKA, IMIE, NAZWISKO, Zarobki)
VALUES (7, 'Andrzej', 'Walenrod', 4500);


INSERT INTO Klient(Id_Klienta, Imie, Nazwisko)
VALUES (1, 'Konrad', 'Brzeczyszczykiewicz');
INSERT INTO Klient(Id_Klienta, Imie, Nazwisko)
VALUES (2, 'Malgorzata', 'Lubiplacki');
INSERT INTO Klient(Id_Klienta, Imie, Nazwisko)
VALUES (3, 'Filip', 'Skromny');
INSERT INTO Klient(Id_Klienta, Imie, Nazwisko)
VALUES (4, 'Pawel', 'Florny');
INSERT INTO Klient(Id_Klienta, Imie, Nazwisko)
VALUES (5, 'Jan', 'Machon');

INSERT INTO SALA(Id_Sali, Ilosc_miejsc, Ilosc_Stolikow)
VALUES (1, 30, 8);

INSERT INTO Kuchnia(Id_Kuchni, Rodzaj_dan, Ilosc_Pracownikow)
VALUES (1, 'Wegetarianskie', 1);
INSERT INTO Kuchnia(Id_Kuchni, Rodzaj_dan, Ilosc_Pracownikow)
VALUES (2, 'Meksykanskie', 1);
INSERT INTO Kuchnia(Id_Kuchni, Rodzaj_dan, Ilosc_Pracownikow)
VALUES (3, 'Wloskie', 1);

INSERT INTO Pracownik_Kuchni(Id_PracownikaKuchni, Id_Pracownika, Id_Kuchni, Stanowisko, Zmiana_Koniec, Zmiana_Poczatek)
VALUES (1, 2, 1, 'Kucharz', 7.00, 15.00);
INSERT INTO Pracownik_Kuchni(Id_PracownikaKuchni, Id_Pracownika, Id_Kuchni, Stanowisko, Zmiana_Koniec, Zmiana_Poczatek)
VALUES (2, 4, 2, 'Starszy Kucharz', 9.00, 17.00);
INSERT INTO Pracownik_Kuchni(Id_PracownikaKuchni, Id_Pracownika, Id_Kuchni, Stanowisko, Zmiana_Koniec, Zmiana_Poczatek)
VALUES (3, 6, 3, 'Kierownik', 7.30, 15.30);

INSERT INTO Pracowni_Sali(Id_PracownikaSali, Id_Pracownika, Id_Sali, Stanowisko, Zmiana_Koniec, Zmiana_Poczatek)
VALUES (1, 1, 1, 'Kelner', 7.30, 15.30);
INSERT INTO Pracowni_Sali(Id_PracownikaSali, Id_Pracownika, Id_Sali, Stanowisko, Zmiana_Koniec, Zmiana_Poczatek)
VALUES (2, 3, 1, 'Kelner', 9.30, 17.30);
INSERT INTO Pracowni_Sali(Id_PracownikaSali, Id_Pracownika, Id_Sali, Stanowisko, Zmiana_Koniec, Zmiana_Poczatek)
VALUES (3, 5, 1, 'Kierownik', 10.00, 18.00);
INSERT INTO Pracowni_Sali(Id_PracownikaSali, Id_Pracownika, Id_Sali, Stanowisko, Zmiana_Koniec, Zmiana_Poczatek)
VALUES (4, 7, 1, 'Zastepca Kierownika', 7.00, 15.00);

INSERT INTO Menu_Dnia(Ilosc_dan, Dania, Id_Sali)
VALUES (10, 'Ostre', 1);
INSERT INTO Menu_Dnia(Ilosc_dan, Dania, Id_Sali)
VALUES (15, 'Lagodne', 1);
INSERT INTO Menu_Dnia(Ilosc_dan, Dania, Id_Sali)
VALUES (5, 'Mieszane', 1);


INSERT INTO Rezerwacja(Id_Rezerwacji, Ilosc_Osob, Data, Id_Klienta)
VALUES (3214, 5, TO_TIMESTAMP_TZ('2020-05-12 16:32', 'YYYY-MM-DD HH24:MI.FF'), 5);
INSERT INTO Rezerwacja(Id_Rezerwacji, Ilosc_Osob, Data, Id_Klienta)
VALUES (321, 8, TO_TIMESTAMP_TZ('2020-07-12 13:32', 'YYYY-MM-DD HH24:MI.FF'), 1);
INSERT INTO Rezerwacja(Id_Rezerwacji, Ilosc_Osob, Data, Id_Klienta)
VALUES (523, 5, TO_TIMESTAMP_TZ('2020-05-23 18:24', 'YYYY-MM-DD HH24:MI.FF'), 1);
INSERT INTO Rezerwacja(Id_Rezerwacji, Ilosc_Osob, Data, Id_Klienta)
VALUES (645, 10, TO_TIMESTAMP_TZ('2020-02-02 14:54', 'YYYY-MM-DD HH24:MI.FF'), 3);
INSERT INTO Rezerwacja(Id_Rezerwacji, Ilosc_Osob, Data, Id_Klienta)
VALUES (32, 5, TO_TIMESTAMP_TZ('2020-12-21 18:00', 'YYYY-MM-DD HH24:MI.FF'), 3);
INSERT INTO Rezerwacja(Id_Rezerwacji, Ilosc_Osob, Data, Id_Klienta)
VALUES (1, 10, TO_TIMESTAMP_TZ('2020-04-29 16:38', 'YYYY-MM-DD HH24:MI.FF'), 5);
INSERT INTO Rezerwacja(Id_Rezerwacji, Ilosc_Osob, Data, Id_Klienta)
VALUES (765, 8, TO_TIMESTAMP_TZ('2020-01-02 16:22', 'YYYY-MM-DD HH24:MI.FF'), 2);
INSERT INTO Rezerwacja(Id_Rezerwacji, Ilosc_Osob, Data, Id_Klienta)
VALUES (12, 2, TO_TIMESTAMP_TZ('2020-12-30 19:43', 'YYYY-MM-DD HH24:MI.FF'), 4);


INSERT INTO Dania(Id_Dania, Rodzaj_Dania, Id_Kuchni, Dnia_Ilosc_Dan, CenaZaDanie)
VALUES (1, 'Dzieciece', 1, 5, 25);
INSERT INTO Dania(Id_Dania, Rodzaj_Dania, Id_Kuchni, Dnia_Ilosc_Dan, CenaZaDanie)
VALUES (2, 'Imprezowe', 3, 15,32);
INSERT INTO Dania(Id_Dania, Rodzaj_Dania, Id_Kuchni, Dnia_Ilosc_Dan, CenaZaDanie)
VALUES (3, 'Powazne', 2, 10, 48);


INSERT INTO Specyfikacje(Id_Rezerwacji, Id_Specyfikacji, Id_Dania, LACZNA_CENA)
VALUES (3214, 1, 3, 300);
INSERT INTO Specyfikacje(Id_Rezerwacji, Id_Specyfikacji, Id_Dania, LACZNA_CENA)
VALUES (321, 2, 1, 240);
INSERT INTO Specyfikacje(Id_Rezerwacji, Id_Specyfikacji, Id_Dania, LACZNA_CENA)
VALUES (523, 3, 2, 185);
INSERT INTO Specyfikacje(Id_Rezerwacji, Id_Specyfikacji, Id_Dania, LACZNA_CENA)
VALUES (645, 4, 3, 500);
INSERT INTO Specyfikacje(Id_Rezerwacji, Id_Specyfikacji, Id_Dania, LACZNA_CENA)
VALUES (32, 5, 3, 242);
INSERT INTO Specyfikacje(Id_Rezerwacji, Id_Specyfikacji, Id_Dania, LACZNA_CENA)
VALUES (1, 6, 1, 340);
INSERT INTO Specyfikacje(Id_Rezerwacji, Id_Specyfikacji, Id_Dania, LACZNA_CENA)
VALUES (765, 7, 2, 248);
INSERT INTO Specyfikacje(Id_Rezerwacji, Id_Specyfikacji, Id_Dania, LACZNA_CENA)
VALUES (12, 8, 1, 67);

--Polecenie Update z warunkiem where

UPDATE  Klient
SET Imie = 'Jan'
WHERE  Nazwisko = 'Lubiplacki';

--Polecenie Delete z warunkiem where

Delete
FROM Pracowni_Sali
WHERE ID_PRACOWNIKA = 1;

--Polecenie Select z podzapytaniem Skrolowanym (SPRAWDZENIE KTORE ID_REZERWACJI ZAPLACI NAJMNIEJ ZA DANE ID_DANIA)

SELECT ID_REZERWACJI, ID_DANIA,LACZNA_CENA
FROM SPECYFIKACJE e
WHERE e.LACZNA_CENA = (SELECT MIN(e2.LACZNA_CENA)
                        FROM SPECYFIKACJE e2
                        WHERE e2.ID_DANIA = e.ID_DANIA);
                        

SELECT *
From Specyfikacje e
WHERE e.ID_Specyfikacji = (Select MIN(e2.ID_Specyfikacji)
                            FROM Specyfikacje e2
                            WHERE e2.ID_Dania = 1);
                            
--Polecenie Select z podzapytaniem (Znalezienie najmniejszego ID_Rezerwacji dla danego ID_Dania)

SELECT *
FROM Specyfikacje e
Where (e.ID_REZERWACJI, e.ID_Dania) IN (SELECT MIN(ID_REZERWACJI), ID_Dania
                                            FROM Specyfikacje
                                            GROUP BY ID_Dania);
                                            
--Funkcja agregujaca z zlaczeniem tabeli (wyliczenie sredniej ceny na osobe)
SELECT CAST(AVG(e.LACZNA_CENA/q.ILOSC_OSOB) AS DECIMAL(10, 2))  CENA_NA_OSOBE, q.ILOSC_OSOB
FROM SPECYFIKACJE e INNER JOIN REZERWACJA q ON e.ID_REZERWACJI = q.ID_REZERWACJI
GROUP BY q.ILOSC_OSOB;
                               
---------------------------------------------------------------------------------------                                            

SELECT ID_SPECYFIKACJI, q.ILOSC_OSOB, q.ID_REZERWACJI, CAST((LACZNA_CENA / ILOSC_OSOB) AS DECIMAL (10, 2)) CENA_NA_OSOBE
FROM SPECYFIKACJE e LEFT JOIN REZERWACJA q ON e.ID_REZERWACJI = q.ID_REZERWACJI
GROUP BY e.ID_SPECYFIKACJI, q.ILOSC_OSOB, q.ID_REZERWACJI, ID_SPECYFIKACJI, LACZNA_CENA
ORDER BY e.ID_SPECYFIKACJI; 
