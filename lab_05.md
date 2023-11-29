# Zadania lab05
## Zadanie 1
* a
```sql
delete from postac
where nazwa <> 'Bjorn'
and rodzaj ='wiking'
order by data_ur asc limit 2;
```
* b
```sql
alter table przetwory drop foreign key przetwory_ibfk_2;

alter table postac drop primary key;
```
## Zadanie 2
* a
```sql
alter table postac add column pesel char(11) first;
update postac set pesel='53817293811' + id_postaci;
alter table postac add primary key (pesel);
```
* b
```sql
alter table postac change rodzaj rodzaj enum('wiking','ptak','kobieta','syrena') DEFAULT NULL;
```
* c
```sql
insert into postac values(53817293819, 9, 'Gertruda Nieszczera', 'syrena', '1909-10-10', 14, default, default);
```
## Zadanie 3
* a
```sql
update postac set statek='Hakon' where nazwa like '%a%';
```
* b
```sql
update statek set max_ladownosc=max_ladownosc * 0.7
where year(data_wodowania)  between 1601
and 1700;
```
* c
```sql
alter table postac add check(wiek < 1000);
```
## Zadanie 4
* a
```sql
alter table postac change rodzaj rodzaj enum('wiking','ptak','kobieta','syrena','wąż') DEFAULT NULL;
insert into postac values(53817293820, 10, 'Loko', 'wąż', '1992-10-10', 100, default, default);
```
* b
```sql
create table marynarz like postac;
insert into marynarz select * from postac
where statek is not null;
```
* c
```sql
alter table marynarz add foreign key (statek) references statek(nazwa_statku);
```
## Zadanie 5
* a
```sql
update postac set jaki_statek=null;
```
* b
```sql
delete from postac
where nazwa <> 'Bjorn'
and rodzaj ='wiking'
order by data_ur asc limit 1;
```
* c
```sql
alter table marynarz drop foreign key marynarz_ibfk_1;
delete from statek;
```
* d
```sql
alter table postac drop foreign key postac_ibfk_1;
drop table statek;
```
* e
```sql
create table zwierz(id_postaci int auto_increment primary key, nazwa varchar(40), wiek int unsigned);
```
* f
```sql
insert into zwierz select id_postaci, nazwa, wiek from postac
where rodzaj = 'ptak';
insert into zwierz select  id_postaci, nazwa, wiek from postac
where rodzaj = 'wąż';
```
