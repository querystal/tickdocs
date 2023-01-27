Use the `SELECT` command to retrieve rows from a table or materialized view. It returns the rows that satisfy the creteria that you specify with the clauses and conditions in your query.

## Syntax
```sql
SELECT [ ALL | DISTINCT ] [ * | expression [ AS output_name ] [ , expression [ AS output_name ] ... ] ]
    [ FROM from_item [ , from_item ...] ]
    [ WHERE condition ]
    [ GROUP BY grouping_expression [ , grouping_expression ... ] ]
    [ HAVING condition ]
    [ ORDER BY sort_expression [ ASC | DESC ] [ , ... ] ]
    [ LIMIT count_number ]
    [ OFFSET start [ ROW | ROWS ] ];
```

```sql
Where from_item can be:

    table_name  [ [ AS ] alias [ ( column_alias_list ) ] ]
    window_type ( table_name, col_name, interval_expression ) [ [ AS ] alias [ ( column_alias_list ) ] ] 
    ( SELECT ) [ [ AS ] alias [ ( column_alias_list ) ] ] 
    from_item join_type from_item [ ON join_condition ]
```
## Parameters
Parameter or clause	Description
expression	A column or an expression.
alias	A temporary alternative name for a table or materialized view in a query.
table_name	A table or materialized view.
grouping_expression	
Values can be:

Input column names
Input column expressions without subqueries or correlated columns
ORDER BY clause	The default sort order is ASC. Nulls options are not supported now. If the sort order is ASC or unspecified, nulls will be placed in front of non-null values. If the sort order is DESC, nulls will be placed after non-null values. This is different from the sort logic in PostgreSQL.
sort_expression	
Values can be:

Output column names
Output column ordinal numbers
Hidden select expressions
LIMIT clause	When the ORDER BY clause is not present, the LIMIT clause cannot be used as part of a materialized view.
count_number	The number of results you want to get.
OFFSET clause	The OFFSET clause can only be used with the LIMIT and ORDER BY clauses.
(SELECT)	A SELECT command. You must enclose the subquery in parentheses, and specify an alias. When you include a subquery in the FROM clause, the output of the subquery is used as a temporary view that is only valid in the query.
join_type	
Supported join types:

[INNER] JOIN
LEFT [OUTER] JOIN
RIGHT [OUTER] JOIN
FULL [OUTER] JOIN
Currently, only the ON clause is supported for joins.

join_condition	Conditions for the ON clause that must be met before the two from_items can be joined.
window_type	The type of the time window function. Possible values are HOP and TUMBLE.
interval_expression	The interval expression, in the format of INTERVAL '<interval>'. For example: INTERVAL '2 MINUTES'. The standard SQL format, which places time units outside of quotation marks (for example, INTERVAL '2' MINUTE), is also supported.

## Example
Below are the tables within the same schema that we will be writing queries from.

The table taxi_trips includes the columns id, distance, duration, and fare, where id identifies each unique trip.

```json
{
  "id": VARCHAR,
  "distance": DOUBLE PRECISION,
  "duration": DOUBLE PRECISION,
  "fare": DOUBLE PRECISION
}
```

The table taxi includes the columns taxi_id and trip_id, where trip_id and id in taxi_trips are matching fields.

```json
{
  "taxi_id": VARCHAR,
  "trip_id": VARCHAR
}
```

The table company includes the columns company_id and taxi_id, where taxi_id and taxi_id in taxi are matching fields.

```json
{
  "company_id": VARCHAR,
  "taxi_id": VARCHAR
}
```

The following query returns the total distance and duration of trips that are beyond the initial charge ($2.50) of each taxi from the company "Yellow Taxi" and "FabCab".

```sql
SELECT 
    taxi.taxi_id, 
    sum(trips.distance) AS total_distance, 
    sum(trips.duration) AS total_duration
FROM taxi_trips AS trips
LEFT JOIN taxi ON trips.id = taxi.trip_id
WHERE taxi_id IN (
          SELECT taxi_id
          FROM company
          WHERE company_id IN ('Yellow Taxi', 'FabCab')
      )
      AND trips.fare > 2.50
GROUP BY taxi_id
ORDER BY total_distance, total_duration;
```
