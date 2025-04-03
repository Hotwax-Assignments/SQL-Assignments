## 4. Product IDs Across Systems

## Business Problem:
### To sync an order or product across multiple systems (e.g., Shopify, HotWax, ERP/NetSuite), the OMS needs to know each system’s unique identifier for that product. This query retrieves the Shopify ID, HotWax ID, and ERP ID (NetSuite ID) for all products.

## Fields to Retrieve:
1. PRODUCT_ID (internal OMS ID)
2. SHOPIFY_ID
3. HOTWAX_ID
4. ERP_ID or NETSUITE_ID (depending on naming)

## Solution:- 
```sql
SELECT p.product_id, g.id_value  AS shopify_id, p.product_id AS hotwax_id, g.good_identification_type_id AS netsuite_id
FROM PRODUCT AS p
JOIN GOOD_IDENTIFICATION AS g ON p.product_id = g.product_id
WHERE g.good_identification_type_id IN ('ERP_ID', 'SHOPIFY_PROD_ID') AND g.id_value IS NOT NULL;
```
![alt text](image.png)

## Query Cost: 922535.44