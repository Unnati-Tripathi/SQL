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
