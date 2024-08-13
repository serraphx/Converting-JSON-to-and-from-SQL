# Converting-JSON-to-and-from-SQL
## Discription
Use the OPENJSON function to translate the following JSON object to a relational format and then insert the translated JSON into a table called JSON_CUSTOMER
```json
{"product_id": 2, "info": {"brand": "Jordan", "name": "AJKO 1"}, "price": 150},
{"product_id": 5, "info": {"brand": "Jordan", "name": "Jumpman MVP"}, "price": 165}
```
Then use JSON PATH to translate the rows and columns in the JSON_CUSTOMER table back to JSON format.

## Languages and Utilities Used

- **Microsoft SQL** 

## Environments Used

- **Windows 10**

## Assignment walk-through:
1. Translates the JSON object to a relational format b assigning json string to a variable "@json"
```SQL
DECLARE @json NVARCHAR(MAX);

SET @json = N'[
	{"product_id": 2, "info": {"brand": "Jordan", "name": "AJKO 1"}, "price": 150},
	{"product_id": 5, "info": {"brand": "Jordan", "name": "Jumpman MVP"}, "price": 165}
]';
```
[photo 1]()

2. Selects data from the json document and inputs it to a table "json_customer"
```SQL
SELECT *
INTO json_customer
FROM OPENJSON(@json) WITH (
	product_id INT '$.product_id',
	brand NVARCHAR(50) '$.info.brand',
	shoe_name NVARCHAR(50) '$.info.name',
	price INT '$.price');
```
3. Returns a json document from a table "json_customer"
```SQL
SELECT product_id AS "$.product_id",
	price AS "$.price",
	brand AS "$.info.brand",
	shoe_name AS "$.info.shoe_name"
FROM json_customer
FOR JSON PATH;
```
[photo 2]()
