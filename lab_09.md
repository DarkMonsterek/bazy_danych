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
