# lab09
## Zadanie 1
```sql
DELIMITER //
CREATE TRIGGER kreatura_before_insert
BEFORE INSERT ON kreatura
FOR EACH ROW
BEGIN
  IF NEW.waga <= 0
  THEN
    SET NEW.waga = 1;
  END IF;
END
//
DELIMITER ;
```
## Zadanie 2
```sql
create table archiwum_wypraw(id_wyprawy int Primary key,
nazwa varchar(100), data_rozpoczecia date,
data_zakonczenia date, kierownik varchar(100));

DELIMITER //
CREATE TRIGGER wyprawa_before_delete
BEFORE delete ON wyprawa
FOR EACH ROW
BEGIN
  insert into archiwum_wypraw
  select w.id_wyprawy, w.nazwa, w.data_rozpoczecia, w.data_zakonczenia, k.nazwa
  from wyprawa w
  inner join kreatura k on w.kierownik=k.idKreatury
  where id_wyprawy=old.id_wyprawy;
END
//
DELIMITER ;
```
## Zadanie 3
```sql
DELIMITER $$
CREATE PROCEDURE eliksir_sily(IN id int)
BEGIN
Update kreatura set udzwig = 1.2 * udzwig where idKreatury = id;
END
$$
DELIMITER ;
```
wywołanie procedury
```sql
call eliksir_sily(1);
```
## Zadanie 4
```sql
create table system_alarmowy(id_alarmu int, wiadomosc varchar(100));


DELIMITER $$

CREATE TRIGGER uczestnicy_after_insert
AFTER INSERT ON uczestnicy
FOR EACH ROW
BEGIN
	DECLARE tesciowa varchar(100);
	DECLARE sektor_id integer;
	DECLARE czy_tesciowa bool;
	DECLARE czy_chata_dziadka bool;
	SET tesciowa = 'Tesciowa';
	SET sektor_id = 7;
	

    
IF tesciowa in (
	SELECT nazwa from kreatura WHERE idKreatury in 
	( SELECT id_uczestnika from uczestnicy where id_wyprawy=NEW.id_wyprawy)) 
	
THEN 
    
	SET czy_tesciowa = true;
	END IF;
    
IF sektor_id in (
	SELECT sektor FROM etapy_wyprawy WHERE idWyprawy=NEW.id_wyprawy
	) 
THEN 
	SET czy_chata_dziadka = true;
END IF;
    
IF czy_tesciowa AND czy_chata_dziadka
    
THEN  
	INSERT INTO system_alarmowy VALUES(default,'Tesciowa nadchodzi',default);
END IF;

END
$$

DELIMITER ;
```
