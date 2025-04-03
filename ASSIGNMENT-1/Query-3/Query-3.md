## 3.Products Missing NetSuite ID

## Business Problem:
### A product cannot sync to NetSuite unless it has a valid NetSuite ID. The OMS needs a list of all products that still need to be created or updated in NetSuite.

## Fields to Retrieve:
1. PRODUCT_ID
2. INTERNAL_NAME
3. PRODUCT_TYPE_ID
4. NETSUITE_ID (or similar field indicating the NetSuite ID; may be NULL or empty if missing)

## Solution:-

```sql 
SELECT p.product_id, p.product_type_id, p.internal_name, g.good_identification_type_id AS netsuite_id
FROM PRODUCT AS p
JOIN PRODUCT_TYPE AS pt ON p.product_type_id = pt.product_type_id 
JOIN GOOD_IDENTIFICATION AS g ON p.product_id = g.product_id 
WHERE g.good_identification_type_id = 'ERP_ID' AND (g.id_value IS NULL OR g.id_value = "");
```

![alt text](image.png)

## Query Cost: 3.90