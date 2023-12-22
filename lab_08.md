# Lab 08
## Zadanie 1
* Zadanie 1 pkt1
```sql
insert into kreatura select * from wikingowie.kreatura;
create table uczestnicy as select * from wikingowie.uczestnicy;
create table etapy_wyprawy as select * from wikingowie.etapy_wyprawy;
create table sektor as select * from wikingowie.sektor;
create table wyprawa as select * from wikingowie.wyprawa;
```
* Zadanie 1 pkt2
```sql
select * from wyprawa;
select k.nazwa from kreatura k
left join uczestnicy u on k.idKreatury=u.id_uczestnika
where u.id_uczestnika is null;
```
* Zadanie 1 pkt3
```sql
select w.nazwa, sum(e.ilosc) from uczestnicy u
inner join wyprawa w on u.id_wyprawy=w.id_wyprawy 
inner join kreatura k on u.id_uczestnika=k.idKreatury
inner join ekwipunek e on k.idKreatury=e.idKreatury
group by w.nazwa;
```
## Zadanie 2
* Zadanie 2 pkt1
```sql
select w.nazwa, count(k.idKreatury) as 'liczba uczestnikow',
group_concat(k.nazwa separator ', ') as 'uczestnicy' 
from uczestnicy u inner join wyprawa w on u.id_wyprawy=w.id_wyprawy 
inner join kreatura k on u.id_uczestnika=k.idKreatury 
group by w.nazwa;
```
* Zadanie 2 pkt2
```sql
select ew.idwyprawy, ew.dziennik, s.nazwa as 'nazwa sektora',
k.nazwa as 'kierownik' from etapy_wyprawy ew
inner join sektor s on ew.sektor=s.id_sektora 
inner join wyprawa w on ew.idwyprawy=w.id_wyprawy 
inner join kreatura k on w.kierownik=k.idKreatury 
order by w.data_rozpoczecia asc, ew.kolejnosc asc;
```
## Zadanie 3
* Zadanie 3 pkt1
```sql
select s.nazwa, ifnull(count(ew.sektor),0) as 'ilosc odwiedzin sektora'
from sektor s 
left join etapy_wyprawy ew on s.id_sektora=ew.sektor
group by s.nazwa;
```
* Zadanie 3 pkt2
```sql
select k.nazwa, if(count(u.id_uczestnika)>0,
'bral udzial w wyprawie',
'nie bral udzialu w wyprawie') czy_bral_udzial
from kreatura k 
left join uczestnicy u on u.id_uczestnika=k.idKreatury
group by k.nazwa;
```
## Zadanie 4
* Zadanie 4 pk1
```sql
select w.nazwa, sum(length(ew.dziennik)) as 'dlugosc' from wyprawa w 
inner join etapy_wyprawy ew on w.id_wyprawy=ew.idWyprawy
group by w.nazwa having dlugosc<400 ;
```
* Zadanie 4 pkt2
```sql
select u.id_wyprawy, w.nazwa, sum(z.waga*e.ilosc)/count(distinct u.id_uczestnika) as 'srednia waga zasobow'
from uczestnicy u
inner join wyprawa w on u.id_wyprawy=w.id_wyprawy 
inner join ekwipunek e on u.id_uczestnika=e.idKreatury
inner join zasob z on e.idZasobu=z.idZasobu
group by u.id_wyprawy, w.nazwa;
```
## Zadanie 5
* Zadanie 5 pkt1
```sql
select w.id_wyprawy,k.nazwa, datediff(w.data_rozpoczecia, k.dataUr) as 'dni kreatury' from kreatura k
inner join uczestnicy u on k.idKreatury=id_uczestnika
inner join wyprawa w on u.id_wyprawy=w.id_wyprawy
inner join etapy_wyprawy ew on ew.idWyprawy=w.id_wyprawy
inner join sektor s on s.id_sektora=ew.sektor
where s.nazwa='Chatka dziadka';
```
