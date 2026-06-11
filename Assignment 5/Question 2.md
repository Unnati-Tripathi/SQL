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
