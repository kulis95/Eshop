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
- Przyk�adowe zapytania
    - POST /api/v1/customers/{customerId}/orders
        - customerId: 3fa85f64-5717-4562-b3fc-2c963f66afa6
        - products id bazuje na `ProductPriceDataApi`
        ```json
        {
          "products": [
            {
              "id": "514f6265-a9b8-46da-a31d-50f4f4c20911", 
              "quantity": 1
            }
          ]
        }
        ```
    - POST /api/v1/customers/{customerId}/orders
        - customerId: 3fa85f64-5717-4562-b3fc-2c963f66afa6
        - products id bazuje na `ProductPriceDataApi`
        ```json
        {
          "products": [
            {
              "id": "514f6265-a9b8-46da-a31d-50f4f4c20911", 
              "quantity": 1
            },
            {
              "id": "514f6265-a9b8-46da-a31d-50f4f4c20912", 
              "quantity": 2
            }
          ]
        }
        ```
    - GET /api/v1/orders/{orderId}
        - orderd: Warto�� zwr�cona przez zapytanie POST
        
- Z powod�w technicznych (serializacja) wszystkie w�a�ciwo�ci modeli domnenowych musz� mie� settery i gettery np. `public Guid Id { get; private set; }`

### Ocena 3.5: Tworzenie nowych u�ytkownik�w
Twoim zadaniem jest zaimplementowanie funkcjonalno�ci tworzenia nowych u�ytkownik�w przy u�yciu agregatu `Customer`.
1. Utw�rz klasy `CreateCustomerCommand` i `GetCustomerQuery`.
2. Zaimplementuj obs�ug� tych komend i zapyta�.
3. Dodaj odpowiednie endpointy do API.
4. Upewnij si�, �e po stworzeniu klienta generowane jest zdarzenie `CustomerCreatedEvent`.

Pami�taj aby stworzy� now� kolekcj� dla tego u�ytkonik�w w bazie danych. 

Zwr�� szczegeg�ln� uwag� na aby do warstwy API nie dosta�y si� modele domenowe!

### Ocena 4.0: Implementacja regu� biznesowych
Stw�rz nast�puj�ce regu�y biznesowe (np. `OrderMustHaveAtLeastOneProductRule`):
1. Nazwa u�ytkownika nie mo�e by� pusta i powinna sk�ada� si� tylko z liter.
2. ��czny koszt produkt�w w zam�wieniu nie mo�e przekroczy� 15000.

### Ocena 5.0: Obs�uga koszyka produkt�w
Twoim zadaniem jest zaimplementowanie obs�ugi koszyka produkt�w.
1. Stw�rz nowy agregat do obs�ugi koszyka z produktami (Tylko dodawanie nowych produkt�w do koszyka).
2. Dodaj odpowiednie komendy (commands) i zapytania (queries) do zarz�dzania koszykiem.
3. Dodaj odpowiednie endpointy do API.
4. Przer�b implementacj� `Order`, aby by�a twrzona w za pomoc� nast�puj�cej metody `public static Order Create(CheckoutCart checkoutCart)`

**Uwaga:** Utw�rz now� kolekcj� dla tej funkcjonalno�ci w bazie danych.