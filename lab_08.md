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
