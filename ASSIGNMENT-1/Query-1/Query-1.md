## 1. New Customers Acquired in June 2023

## Business Problem:
### The marketing team ran a campaign in June 2023 and wants to see how many new customers signed up during that period.

## Fields to Retrieve:
1. PARTY_ID
2. FIRST_NAME
3. LAST_NAME
4. EMAIL
5. PHONE
6. ENTRY_DATE

## Solution:-
```sql
SELECT per.party_id, per.first_name, per.last_name, cm.info_string, tn.contact_number, per.created_stamp
FROM PARTY_ROLE as pr 
JOIN PERSON as per ON pr.party_id = per.party_id AND role_type_id='CUSTOMER'
JOIN PARTY_CONTACT_MECH AS pcm ON  per.party_id = pcm.party_id
LEFT JOIN CONTACT_MECH AS cm ON pcm.contact_mech_id = cm.contact_mech_id AND cm.contact_mech_type_id IN ('EMAIL_ADDRESS', 'TELECOM_NUMBER')
LEFT JOIN TELECOM_NUMBER AS tn ON cm.contact_mech_id = tn.contact_mech_id
WHERE per.created_stamp between '2023-06-01 00:00:00' AND '2023-06-30 23:59:59';
```

![alt text](image.png)

## Query Cost: 16092.95
