`SELECT` is the only SQL statement allowed by users. It is simply to use a query to build up all you need.

## Synopsis
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
