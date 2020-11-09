# gemma-dbt-utils
Gemma Analytics utilities for dbt

This packages is expected to be used in addition to [dbt-utils](https://github.com/fishtown-analytics/dbt-utils) and expands upon it rather than replacing it.

## TBU
- Licence
- Properly implement integration tests

## Schema Tests

### numeric_constraints ([source](macros/schema_tests/numeric_constraints.sql))
This schema test asserts that a column of numerical value is within specified bounds.

Usage:
```yaml
version: 2
models:
  - name: model_name
    columns:
      - name: a_number
        tests:
          - gemma_dbt_utils.numeric_constraints:
              gte: 0
              lt: 180
```

Possible options:
```
eq:   equal
ne:   not equal
gt:   greater than
gte:  greater than or equal
lt:   lower than
lte:  lower than or equal
```

The macro accepts an optional parameter `condition` that allows for asserting
the `expression` on a subset of all records.

Usage:
```yaml
version: 2
models:
  - name: model_name
    columns:
      - name: a_number
        tests:
          - gemma_dbt_utils.numeric_constraints:
              eq: 1
              condition: "status = 'success'"
```
