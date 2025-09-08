---

---
---

-- Horário local 

```
SELECT extract(hourfromnow()ATTIMEZONE'America/Sao_Paulo')||':'|| 
extract(minfromnow()ATTIMEZONE'America/Sao_Paulo')||':'|| 
round(extract(secfromnow()ATTIMEZONE'America/Sao_Paulo'),0)"Horário Local" 
```


---

-- Extração de tempo

Ano:
```
select extract(year from [colun]) 
```

Mês:
```
select extract(month from [colun]) 
```

Dia:
```
select extract(day from [colun]) 
```

---------------------

