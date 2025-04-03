## 2. List All Active Physical Products

## Business Problem:
### Merchandising teams often need a list of all physical products to manage logistics, warehousing, and shipping.

## Fields to Retrieve:
1. PRODUCT_ID
2. PRODUCT_TYPE_ID
3. INTERNAL_NAME

## Solution:
```sql
SELECT p.product_id, p.product_type_id, p.internal_name
FROM PRODUCT AS p
JOIN PRODUCT_TYPE AS pt ON p.product_type_id = pt.product_type_id
WHERE pt.is_physical='Y' AND p.sales_discontinuation_date IS NULL AND p.support_discontinuation_date IS NULL;
```

![alt text](image.png)

## Query Cost: 80649.63