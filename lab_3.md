# Lab 03 Część 2
## Zadanie 1
```sql
select d.nazwa, min(p.pensja), max(p.pensja), avg(p.pensja) from dzial d 
inner join pracownik p on d.id_dzialu=p.dzial group by id_dzialu;
```
## Zadanie 2
```sql
select k.pelna_nazwa, sum(pz.cena*pz.ilosc) as wartosc_zamowienia from klient k 
inner join zamowienie z on k.id_klienta=z.klient
inner join pozycja_zamowienia pz on z.id_zamowienia=pz.zamowienie 
group by pz.zamowienie
order by wartosc_zamowienia desc limit 10;
```
## Zadanie 3
```sql
select Year(z.data_zamowienia) as Rok, sum((pz.cena-t.cena_zakupu)*pz.ilosc) as przychod from zamowienie z 
inner join pozycja_zamowienia pz on z.id_zamowienia=pz.zamowienie
inner join towar t on pz.towar=t.id_towaru
group by Year(z.data_zamowienia)
order by sum(pz.cena*pz.ilosc) desc;
```
## Zadanie 4
```
select sum(pz.ilosc*pz.cena) as 'suma wartosci anulowanych zamowien' from status_zamowienia sz 
inner join zamowienie z on sz.id_statusu_zamowienia=z.status_zamowienia
inner join pozycja_zamowienia pz on z.id_zamowienia=pz.zamowienie
where sz.nazwa_statusu_zamowienia = 'anulowane';
```
