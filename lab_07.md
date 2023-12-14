# Lab07
## Zadanie 1
* Zadanie 1 pkt1
```sql
select avg(waga) from kreatura
where rodzaj='wiking';
```
* Zadanie 1 pkt2
```sql
select rodzaj, avg(waga), count(waga),
count(*)
from kreatura group by rodzaj;
```
* Zadanie 1 pkt3
```sql
select rodzaj, avg(year(curdate())-year(dataUr)) as 'średni wiek' 
from kreatura group by rodzaj;
```
## Zadanie 2
* Zadanie 2 pkt1
```sql
select rodzaj, sum(waga*ilosc) from zasob group by rodzaj;
```
* Zadanie 2 pkt2
```sql
select nazwa, avg(waga) from zasob
where ilosc >= 4
group by nazwa having sum(waga) >10 ;
```
* Zadanie 2 pkt3
```sql
select rodzaj, count(distinct(nazwa)) as liczba from zasob
group by rodzaj having liczba >1 ;
```
## Zadanie 3
* Zadanie 3 pkt1
```sql
select k.nazwa, e.idZasobu, e.ilosc from kreatura k
inner join ekwipunek e on k.idKreatury=e.idKreatury;
```
* Zadanie 3 pkt2
```sql
select k.nazwa, z.nazwa from kreatura k
inner join ekwipunek e on k.idKreatury=e.idKreatury
inner join zasob z on z.idZasobu=e.idZasobu;
```
* Zadanie 3 pkt3
```sql
select k.nazwa from kreatura k
left join ekwipunek e on k.idKreatury=e.idKreatury
where e.idKreatury is null;
```
## Zadanie 4
* Zadanie 4 pkt1
```sql
select k.nazwa, z.nazwa from kreatura k, ekwipunek e natural join
zasob z where k.rodzaj='wiking' and year(k.dataUr) between 1670 and 1679;
```
* Zadanie 4 pkt2
```sql
select * from kreatura k
inner join ekwipunek e on k.idKreatury=e.idKreatury
inner join zasob z on z.idZasobu=e.idZasobu
where z.rodzaj='jedzenie'
order by k.dataUr desc limit 5;
```
* Zadanie 4 pkt3
```sql
select concat(k1.nazwa,'-', k2.nazwa)
from kreatura k1
inner join kreatura k2
where k1.idKreatury - k2.idKreatury = 5;
```
## Zadanie 5
* Zaadanie 5 pkt1
```sql
select k.rodzaj, avg(e.ilosc * z.waga) from kreatura k
inner join ekwipunek e on k.idKreatury=e.idKreatury
inner join zasob z on e.idZasobu=z.idZasobu
where k.rodzaj not in ('malpa','waz')
group by k.rodzaj having sum(e.ilosc) <30;
```
* Zadanie 5 pkt2
```sql
select a.nazwa, a.rodzaj, a.dataUr from kreatura a,
(select min(dataUr) min, max(dataUr) max
from kreatura group by rodzaj) b
where b.min = a.dataUr or b.max=a.dataUr;
```
