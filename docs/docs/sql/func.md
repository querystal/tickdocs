## Aggregation

<b>avg(x)</b>
<p>Returns the average (arithmetic mean) of all input values.</p>

<b>count(*)</b>
<p>Returns the number of input rows.</p>

<b>count(x)</b>
<p>Returns the number of non-null input values.</p>

<b>max(x)</b>
<p>Returns the maximum value of all input values.</p>

<b>min(x)</b>
<p>Returns the minimum value of all input values.</p>

<b>sum(x)</b>
<p>Returns the sum of all input values.</p>

## Array
<b>unnest(x)</b>
<p>Flattens an <b>array(array[T])</b> to an <b>array[T]</b> by concatenating the contained arrays.</p>

## Cast
<b>cast (x AS type)</b>
<p>convert the datatype of x into new <b>type</b>.</p>

## Conditional
<b>CASE</b>
```sql
CASE expression
    WHEN value THEN result
    [ WHEN ... ]
    [ ELSE result ]
END
```

```sql
CASE
    WHEN condition THEN result
    [ WHEN ... ]
    [ ELSE result ]
END
```

<b>COALESCE(x)</b>
<p>Returns the first non-null value in the column, or null if all values in this column are null.</p>

<b>NULLIF(value1, value2)</b>
<p>Return null if value1 equals to value2, otherwise returns value1.</p>

## Date / Time

## Logical
|Operator|Description|Example|
|---|---|---|
|AND|True if both values are true|a AND b|
|OR|True if either value is true|a OR b|
|NOT|True if the value is false|NOT a|

## Mathematical
<b>x+y</b>
<p>Addition.</p>
<b>x-y</b>
<p>Substraction.</p>
<b>-x</b>
<p>Negation.</p>
<b>x*y</b>
<p>Multiplication.</p>
<b>x/y</b>
<p>Division.</p>
<b>x%y</b>
<p>Remainder.</p>
<b>xey</b>
<p>Exponential y power to 10 times x.</p>
<b>abs(x)</b>
<p>Returns absolute value of x.</p>
<b>round(x)</b>
<p>Rounds to the nearest integer.</p>
<b>round(x, y)</b>
<p>Rounds x to y decimal places.</p>
<b>floor(x)</b>
<p>Returns the nearest integer less than or equals to the argument.</p>
<b>cell(x)</b>
<p>Returns the nearest integer greater than or equals to the argument.</p>

## Set

## String

## Window