## Zadanie 1
```sql
select imie, nazwisko, data_urodzenia from pracownik;
```
## Zadanie 2
```sql
select imie, nazwisko, Year(curdate())-Year(data_urodzenia) as wiek from pracownik;
```
## Zadanie 3
```sql
select d.nazwa, count(p.id_pracownika) as 'ilosc pracownikow' from dzial d
left join pracownik p on p.dzial=d.id_dzialu group by d.id_dzialu;
```
## Zadanie 4
```sql
select k.nazwa_kategori, count(t.id_towaru) as 'liczba produktow' from kategoria k 
left join towar t on t.kategoria=k.id_kategori group by k.id_kategori;
```
## Zadanie 5
```sql
select k.nazwa_kategori, group_concat(t.nazwa_towaru) as 'lista produktow' from kategoria k 
left join towar t on t.kategoria=k.id_kategori group by k.id_kategori;
```
## Zadanie 6
```sql
select round(avg(pensja), 2) as 'srednia pensja' from pracownik;
```
## Zadanie 7
```sql
select round(avg(pensja), 2) from pracownik
where data_zatrudnienia <= 
subdate(curdate(), interval 5 year);
```
## Zadanie 8
```sql
select t.nazwa_towaru, count(*) as total
from towar t inner join pozycja_zamowienia p
on t.id_towaru=p.towar group by p.towar
order by total desc limit 10;
```
## Zadanie 9
```sql
select z.id_zamowienia, z.numer_zamowienia,
SUM(pz.ilosc*pz.cena)
from zamowienie z inner join pozycja_zamowienia pz
on z.id_zamowienia=pz.zamowienie
where quarter(z.data_zamowienia)=1
and year(z.data_zamowienia)= 2017
group by z.id_zamowienia;
```
## Zadanie 10
```sql
select pr.imie, pr.nazwisko ,
sum(pz.ilosc*pz.cena)
from zamowienie z inner join pozycja_zamowienia pz
on z.id_zamowienia=pz.zamowienie
inner join pracownik pr on pr.id_pracownika=z.pracownik_id_pracownika
group by z.pracownik_id_pracownika;
```
