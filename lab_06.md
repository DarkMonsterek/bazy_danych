# Lab 06
## Zadanie 1
* Zadanie 1 pkt1
```sql
create table kreatura as select * from
wikingowie.kreatura;

create table zasob as select * from
wikingowie.zasob;

create table ekwipunek as select * from
wikingowie.ekwipunek;
```
* Zadanie 1 pkt2
```sql
select * from zasob;
```
* Zadanie 1 pkt 3
```sql
select * from zasob where rodzaj='jedzenie';
```
* Zadanie 1 pkt 4
```sql
select idZasobu, ilosc from zasob where idZasobu in (1,3,5);
```
## Zadanie 2
* Zadanie 2 pkt1
```sql
select * from kreatura where rodzaj <> 'wiedzma' and  udzwig>50 or udzwig=50;
```
* Zadanie 2 pkt2
```sql
select * from zasob where waga between 2 and 5;
```
* Zadanie 2 pkt3
```sql
select * from kreatura where nazwa='%or%' and udzwig between 30 and 70;
```
## Zadanie 3
* Zadanie 3 pkt1
```sql
select * from zasob where month(dataPozyskania) =7 or month(dataPozyskania)=8;
```
* Zadanie 3 pkt2
```sql
select * from zasob where rodzaj is not null order by waga asc;
```
* Zadanie 3 pkt3
```sql
select * from kreatura where dataUr is not null order by dataUr asc limit 5;
```
## Zadanie 4
* Zadanie 4 pkt1
```sql
select distinct rodzaj as 'unikalne rodzaje' from zasob;
```
* Zadanie 4 pkt2
```sql
select concat(nazwa, ' - ', rodzaj) as 'nazwa i rodzaj kreatury' from kreatura where rodzaj like 'wi%';
```
* Zadanie 4 pkt3
```sql
select *, (ilosc*waga) as 'całkowita waga zasobu' from zasob where year(dataPozyskania) between 2000 and 2007;
```
## Zadanie 5
* Zadanie 5 pkt1
```sql
select nazwa, (waga*ilosc*0.7) as 'waga netto', (waga*ilosc*0.3) as 'waga odpadow' from zasob where rodzaj='jedzenie';
```
* Zadanie 5 pkt2
```sql
select * from zasob where rodzaj is null;
```
* Zadanie 5 pkt3
```sql
select distinct rodzaj, nazwa from zasob where nazwa like 'Ba%' or nazwa like '%os'order by nazwa;
```
