# Laboratorium 5: Wprowadzenie do Domain Driven Design (DDD) oraz Command Query Responsibility Segregation (CQRS)

## Cel zadania
Celem tego laboratorium jest praktyczne zapoznanie si� z kluczowymi aspektami Domain Driven Design (DDD) oraz podstawami Command Query Responsibility Segregation (CQRS). Przed rozpocz�ciem, zapoznaj si� z dost�pnym kodem. W razie pyta�, skontaktuj si� przez platform� Teams.

### Wskaz�wki:
- Pami�taj o odpowiednim oddzieleniu warstwy domenowej, aplikacji oraz infrastruktury (w ramach uproszczenia w tym projekcie modele domeny oraz infrastruktury s� takie same).
- Staraj si� trzyma� zasad SOLID w trakcie projektowania klas.
- Projekt uruchamia si� pod adresem http://localhost:8080
- Do po��czenia z baz� danych mo�esz u�y� narz�dzi takich jak Studio3T. Wymagany jest nast�puj�cy ci�g po��czeniowy: `mongodb://root:example@eshop.mongodb:27017`.
- Podczas instalacji Visual Studio upewnij si�, �e zainstalowa�e� pakiet ASP.NET and web development.
- Zachecam do stworzenia klona tego repozytorum, w przypadku potrzeby dodania poprawek z mojej strony b�dzie Pa�stwu �atwiej si� z nimi integrowa�. 

### Ocena 3.5: Tworzenie nowych u�ytkownik�w
Twoim zadaniem jest zaimplementowanie funkcjonalno�ci tworzenia nowych u�ytkownik�w przy u�yciu agregatu `Customer`.
1. Utw�rz klasy `CreateCustomerCommand` i `GetCustomerQuery`.
2. Zaimplementuj obs�ug� tych komend i zapyta�.
3. Dodaj odpowiednie endpointy do API.
4. Upewnij si�, �e po stworzeniu klienta generowane jest zdarzenie `CustomerCreatedEvent`.

Pami�taj aby stworzy� now� kolekcj� dla tego u�ytkonik�w w bazie danych. 

Zwr�� szczegeg�ln� uwag� na aby do warstwy API nie dosta�y si� modele domenowe!

### Ocena 3.5: Implementacja regu� biznesowych
Stw�rz nast�puj�ce regu�y biznesowe (np. `OrderMustHaveAtLeastOneProductRule`):
1. Nazwa u�ytkownika nie mo�e by� pusta i powinna sk�ada� si� tylko z liter.
2. ��czny koszt produkt�w w zam�wieniu nie mo�e przekroczy� 15000.

### Ocena 4.5: Obs�uga koszyka produkt�w
Twoim zadaniem jest zaimplementowanie obs�ugi koszyka produkt�w.
1. Stw�rz nowy agregat do obs�ugi koszyka z produktami.
2. Dodaj odpowiednie komendy (commands) i zapytania (queries) do zarz�dzania koszykiem.
3. Dodaj odpowiednie endpointy do API.
4. Przer�b implementacj� `Order`, aby by�a twrzona w za pomoc� nast�puj�cej metody ```csharp public static Order Create(CheckoutCart checkoutCart) ```


**Uwaga:** Utw�rz now� kolekcj� dla tej funkcjonalno�ci w bazie danych.

### Ocena 5.0: Integracja z innym projektem
Za pomoc� Refit (https://github.com/reactiveui/refit) nawi�� po��czenie z projektem z laboratorium 2, aby pobra� informacje o produktach. Podczas integracji zwr�� uwag� na wykorzystanie kontener�w.

Przyk�adowy interfejs do wykorzystania:

```csharp
public interface IProductsApi
{
    [Get("/products")]
    Task<List<Product>> GetAllProductsAsync();
}
```

Wykorzystaj zaimplementowany interfejs `IProductsApi` w klasie `ProductPriceDataApi`.