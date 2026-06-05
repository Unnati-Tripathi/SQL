# Assignment 1: String Functions and Regular Expressions

---

# Question 1: String Aggregation

## Query

```sql
SELECT
    department_name,
    STRING_AGG(employee_name, ', ' ORDER BY employee_name) AS employee_list
FROM department_employees
GROUP BY department_name
ORDER BY department_name;
```

## My Understanding

Normally, each employee is stored in a separate row.

Example:

| department_name | employee_name |
|---------------|---------------|
| Engineering | Amit Kumar |
| Engineering | Priya Sharma |
| Engineering | Rahul Verma |

Using `STRING_AGG()` we can combine all employee names belonging to the same department into a single comma-separated string.

Output becomes:

```text
Engineering → Amit Kumar, Priya Sharma, Rahul Verma
```

### Functions Used

| Function | Purpose |
|----------|----------|
| `STRING_AGG()` | Combines multiple rows into a single string |
| `GROUP BY` | Creates one result row for each department |
| `ORDER BY employee_name` | Sorts employee names alphabetically inside the list |

---

# Question 2: Camel Case Conversion

## Query

```sql
WITH words AS (
    SELECT
        id,
        word,
        word_position
    FROM text_values
    CROSS JOIN LATERAL
    regexp_split_to_table(lower(input_text), '\s+')
    WITH ORDINALITY AS split_words(word, word_position)
)

SELECT
    id,
    STRING_AGG(
        CASE
            WHEN word_position = 1 THEN word
            ELSE INITCAP(word)
        END,
        ''
        ORDER BY word_position
    ) AS camel_case_text
FROM words
GROUP BY id
ORDER BY id;
```

## My Understanding

Camel case means:

```text
employee full name
```

becomes

```text
employeeFullName
```

### Step 1

Convert the complete text into lowercase.

```text
employee full name
```

### Step 2

Break the sentence into individual words.

```text
employee
full
name
```

### Step 3

Keep the first word as it is.

```text
employee
```

Convert the remaining words using `INITCAP()`.

```text
Full
Name
```

### Step 4

Join all words together without spaces.

```text
employeeFullName
```

### Functions Used

| Function | Purpose |
|----------|----------|
| `lower()` | Converts text into lowercase |
| `regexp_split_to_table()` | Splits a sentence into individual words |
| `WITH ORDINALITY` | Stores the position of each word |
| `INITCAP()` | Capitalizes the first letter of a word |
| `STRING_AGG()` | Joins all words together |

---

# Question 3: Replace Text Using Regular Expression

## Query

```sql
SELECT
    id,
    full_name,
    regexp_replace(
        full_name,
        '\m(amit kumar) (singh)\M',
        '\1_\2',
        'i'
    ) AS updated_name
FROM person_names
ORDER BY id;
```

## My Understanding

Requirement:

```text
amit kumar singh
```

should become

```text
amit kumar_singh
```

Only the space between **kumar** and **singh** should be replaced.

### Before

```text
amit kumar singh
```

### After

```text
amit kumar_singh
```

The regular expression searches for:

```text
amit kumar + space + singh
```

and replaces that space with an underscore (`_`).

`(amit kumar)` becomes **Group 1**.

`(singh)` becomes **Group 2**.

Then:

```text
\1_\2
```

means:

```text
Group1 + "_" + Group2
```

which produces:

```text
amit kumar_singh
```

### Functions Used

| Function | Purpose |
|----------|----------|
| `regexp_replace()` | Finds and replaces matching text |
| `()` | Creates capture groups |
| `\1` | Refers to the first captured group |
| `\2` | Refers to the second captured group |
| `i` | Performs case-insensitive matching |

---
