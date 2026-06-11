# Find out a way to query and store JSON flattened data from one PostgreSQL table to another PostgreSQL table

## Objective

The goal is to read data stored in JSON format inside a PostgreSQL table, extract the required fields, and store them in another table with a structured schema.

This approach is useful when API responses are stored as JSONB and need to be transformed into relational tables for reporting, analytics, or further processing.

## Source Table

The `api_data` table stores incoming API responses in a JSONB column named `payload`.

```sql
CREATE TABLE api_data (
    id SERIAL PRIMARY KEY,
    payload JSONB
);
```

Sample data:

```sql
INSERT INTO api_data (payload) VALUES
('{
  "sale_id": 11,
  "rep_name": "Rohan Bajaj",
  "department": "Engineering",
  "city": "Hyderabad",
  "amount": 78000,
  "status": "open"
}'),
('{
  "sale_id": 12,
  "rep_name": "Pooja Iyer",
  "department": "HR",
  "city": "Chennai",
  "amount": 44000,
  "status": "open"
}');
```

## Target Table

The flattened data will be stored in a structured table.

```sql
CREATE TABLE sales_flattened (
    sale_id INT,
    rep_name TEXT,
    department TEXT,
    city TEXT,
    amount NUMERIC,
    status TEXT
);
```

## Extracting JSON Fields

The `->>` operator is used to extract JSON values as text.

Example:

```sql
SELECT
    payload->>'rep_name' AS rep_name,
    payload->>'city' AS city
FROM api_data;
```

## Flattening and Loading Data

The following query extracts values from the JSON payload, converts them to the appropriate data types, and inserts them into the target table.

```sql
INSERT INTO sales_flattened (
    sale_id,
    rep_name,
    department,
    city,
    amount,
    status
)
SELECT
    (payload->>'sale_id')::INT,
    payload->>'rep_name',
    payload->>'department',
    payload->>'city',
    (payload->>'amount')::NUMERIC,
    payload->>'status'
FROM api_data;
```

## Verification

To confirm that the data has been loaded successfully:

```sql
SELECT *
FROM sales_flattened;
```

## Conclusion

The JSON data stored in the source table can be flattened by extracting individual attributes using JSON operators and then inserting the transformed data into a relational table. This method provides a simple way to convert API response data into a format that is easier to query and analyze.
