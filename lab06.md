```sql
#Lab 06
#zadanie 1
# jezeli wybrana baza to baza imienna
create table kreatura as select * from
wikingowie.kreatura;
# jezeli wybrana baza to wikingowie
#create table infs_.kreatura select * from ;
create table zasob as select * from
wikingowie.zasob;
create table ekwipunek as select * from
wikingowie.ekwipunek;
select * from zasob;
select * from zasob where rodzaj='jedzenie';
select idZasobu, ilosc from zasob where idZasobu in (1,3,5);

#zadanie 2
select * from kreatura;
select * from kreatura where rodzaj <> 'wiedzma' and  udzwig>50 or udzwig=50;
select * from zasob where waga between 2 and 5;
select * from kreatura where nazwa='%or%' and udzwig between 30 and 70;
#zadanie 3
select * from zasob;
select * from zasob where month(dataPozyskania) =7 or month(dataPozyskania)=8;
select * from zasob where rodzaj is not null order by waga asc;
select * from kreatura where dataUr is not null order by dataUr asc limit 5;
#zadanie 4
#select distinct(rodzaj) from kreatura;
select distinct rodzaj as 'unikalne rodzaje' from zasob;
select concat(nazwa, ' - ', rodzaj) as 'nazwa i rodzaj kreatury' from kreatura where rodzaj like 'wi%';
#select concat('Ala', 'ma', 'kota') as zdanie;
#select concat(nazwa, 'to id=', idKreatury) from kreatura;
select *, (ilosc*waga) as 'całkowita waga zasobu' from zasob where year(dataPozyskania) between 2000 and 2007;
#zadanie 5
#select * from zasob where rodzaj='jedzenie';
select nazwa, (waga*ilosc*0.7) as 'waga netto', (waga*ilosc*0.3) as 'waga odpadow' from zasob where rodzaj='jedzenie';
select * from zasob where rodzaj is null;
select distinct rodzaj, nazwa from zasob where nazwa like 'Ba%' or nazwa like '%os'order by nazwa;
```
