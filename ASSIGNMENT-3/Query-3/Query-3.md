## 3.Single-Return Orders (Last Month)

## Business Problem:
### The mechandising team needs a list of orders that only have one return.

## Fields to Retrieve:

1. PARTY_ID
2. FIRST_NAME

## Solution:-
```sql
SELECT rh.from_party_id AS party_id, p.first_name, rh.return_date
FROM RETURN_HEADER AS rh
JOIN PERSON AS p ON p.party_id= rh.from_party_id
WHERE rh.RETURN_DATE >=  DATE_FORMAT(NOW() - INTERVAL 1 MONTH, '%2023-%m-01') AND rh.RETURN_DATE < DATE_FORMAT(NOW(), '%2023-%m-01')
GROUP BY party_id, p.first_name, rh.return_date
HAVING count(rh.return_id)=1;

```
![alt text](image.png)

## Query Cost: 1154.69