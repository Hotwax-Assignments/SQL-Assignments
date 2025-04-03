## 7. Store with Most One-Day Shipped Orders (Last Month)

## Business Problem:
### Identify which facility (store) handled the highest volume of “one-day shipping” orders in the previous month, useful for operational benchmarking.

## Fields to Retrieve:
1. FACILITY_ID
2. FACILITY_NAME
3. TOTAL_ONE_DAY_SHIP_ORDERS
4. REPORTING_PERIOD

## Solution:-
```sql
SELECT f.facility_id, f.facility_name, count(oisg.order_id) AS total_one_day_ship_orders, date_format(oh.order_date, '%m-%y') AS reporting_period
FROM FACILITY AS f
JOIN ORDER_ITEM_SHIP_GROUP AS oisg ON oisg.facility_id= f.facility_id AND oisg.shipment_method_type_id= 'NEXT_DAY'
JOIN ORDER_HEADER AS oh ON oh.order_id= oisg.order_id
WHERE oh.order_date >= date_format(now() - interval 1 month, '2023-%m-01') AND oh.order_date < date_format(now() , '2023-%m-01')
GROUP BY f.facility_id, f.facility_name, reporting_period
ORDER BY total_one_day_ship_orders DESC
LIMIT 1;

```

![alt text](image.png)

## Query Cost: 28113.80