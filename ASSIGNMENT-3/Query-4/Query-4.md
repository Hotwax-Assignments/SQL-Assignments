## 4. Returns and Appeasements

## Business Problem:
### The retailer needs the total amount of items, were returned as well as how many appeasements were issued.

## Fields to Retrieve:
1. TOTAL RETURNS
2. RETURN $ TOTAL
3. TOTAL APPEASEMENTS
4. APPEASEMENTS $ TOTAL

## Solution:-
```sql
SELECT count(ri.return_id) AS total_return, sum(ri.return_quantity * ri.return_price) AS return_total, 
		count(ra.return_adjustment_id) AS total_appeasements, sum(ra.amount) AS apeasements_total
FROM RETURN_ITEM AS ri
JOIN RETURN_ADJUSTMENT AS ra ON ra.return_id= ri.return_id AND ra.return_adjustment_type_id = "APPEASEMENT"
WHERE ri.status_id= 'RETURN_COMPLETED';

```
![alt text](image.png)

## Query Cost: 340.83