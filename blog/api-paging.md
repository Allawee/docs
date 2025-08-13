---
slug: api-paging-and-query-language
title: API Paging and Query Language
# authors: 
tags: [api, query]
---

## API Paging and Query Language

Developer-friendly cursor paging and a compact query language for filtering, sorting, selecting, and expanding resources via REST. Use these query parameters with your HTTP endpoints; no SDK required.

### What you get
- Flexible filter language with short-hand operators and support for spaces/quoting
- Cursor-based pagination with `before`/`after` semantics
- `select` field projection and `expand` for related resources (with per-path selects)
- `sort`, `limit`, `or`/`nor`/`and`
- Optional `countTotal` flag

### How it works
- Compose queries with `filter`, `select`, `expand`, `sort`, `limit`, `before`, `after`, `countTotal`.
- All parameters are URL query parameters; examples below use curl.

## Quick start (REST)

Request the first page with filters, selection and sorting:

```bash
curl -G 'https://api.example.com/customers' \
  --data-urlencode 'filter=email:john@doe.com createdAt|gtd|2024-01-01T00:00:00.000Z' \
  --data-urlencode 'select=id name email' \
  --data-urlencode 'sort=-createdAt' \
  --data-urlencode 'limit=20' \
  --data-urlencode 'countTotal'
```

Paginate forward using `after` (pass the last `id` from the previous page):

```bash
curl -G 'https://api.example.com/customers' \
  --data-urlencode 'filter=email~doe' \
  --data-urlencode 'after=ent_2x9abc' \
  --data-urlencode 'limit=20'
```

## HTTP query parameters

- `limit`: number. Default 20.
- `sort`: space-separated list. Example: `sort=-createdAt publishedAt`.
- `select`: space-separated fields to include/exclude. Example: `select=id name -secret`.
- `expand`: space-separated population paths; use `:` to select subfields. Example: `expand=user:firstName,email posts:title`.
- `filter`: space-separated filter expressions (see grammar below).
- `or`, `nor`, `and`: same syntax as `filter`; combined using OR/NOR/AND logic.
- `before`: id of the last item from the previous page (cursor backward).
- `after`: id of the last item from the current page (cursor forward).
- `countTotal`: boolean. Supports short form: `&countTotal` is treated as `true`.

### Boolean short form
Short form without value is treated as `true`, so `&countTotal` is valid.

## Filter language (for REST queries)

The filter query is a space-separated list of entries. Each entry can be written in long or shorthand form.

### Operators

| Operator | Long form                | Shorthand(s)                   | Meaning                          |
|----------|--------------------------|--------------------------------|----------------------------------|
| eq       | `field|eq|value`         | `field:value`, `field=value`   | Equals                           |
| ne       | `field|ne|value`         | `-field:value`, `field!=value` | Not equals                       |
| gt       | `field|gt|N`             | `field>N`                      | Greater than                     |
| gte      | `field|gte|N`            | `field>=N`                     | Greater than or equal            |
| lt       | `field|lt|N`             | `field<N`                      | Less than                        |
| lte      | `field|lte|N`            | `field<=N`                     | Less than or equal               |
| like     | `field|like|text`        | `field~text`                   | Case-insensitive regex match     |
| nlike    | `field|nlike|text`       | `-field~text`                  | Not match (case-insensitive)     |
| in       | `field|in|a,b,c`         | —                              | In list                          |
| nin      | `field|nin|a,b,c`        | —                              | Not in list                      |
| all      | `field|all|a,b,c`        | —                              | Array contains all values        |
| size     | `field|size|N`           | —                              | Array size equals N              |
| nsize    | `field|nsize|N`          | —                              | Array size not N                 |
| exists   | `field|exists|true`      | —                              | Field exists (boolean)           |

Numbers are parsed safely; non-numeric values remain strings.

### Date operators

For common date fields (e.g., `createdAt`, `updatedAt`, `txTime`, `date`):

- `gtd` -> greater than date: `createdAt|gtd|2020-01-01T00:00:00.000Z`
- `gted` -> greater than or equal date
- `ltd` -> less than date
- `lted` -> less than or equal date

Tip: You can also use numeric operators (e.g., `createdAt>=2020-01-01T...`).

### Grouping with OR/NOR/AND

Use separate params to group expressions:

```
?filter=state:active amount>1000
&or=country:NG country:GH
&nor=channel:manual
&and=verified:true
```

Each param uses the same space-separated grammar as `filter` and is converted to `$or`, `$nor`, and `$and` blocks.

### Quoting and spaces

- Wrap values with spaces in quotes or angle brackets:
  - `name:"John Doe"`
  - `name:<John Doe>`
- Escape `"` or `>` inside quoted/bracketed values with a backslash: `name:"John \"JD\" Doe"`

### Identifier fields

You can filter by identifiers such as `id`, `customer`, `card`, `account`, `program`, `event`, or `bin`. Nested identifiers are supported using dot notation (e.g., `customer.id`). Examples:

```
filter=customer|eq|cus_abc123
filter=customer.id|eq|us_xyz123
filter=account|in|acc_1,acc_2,acc_3
```

## Select and expand

### select
- Space-separated list of fields to include/exclude (prefix with `-` to exclude).
- Depth is limited to 1 by default; deeper paths may be truncated.

Examples:
```
select=id name -secret source
```

### expand (include related)
- Space-separated paths; use dot-notation for nesting (max depth 2 by default).
- Use `:` to specify fields of the populated path: `expand=user:firstName,email`.
- Multiple selects for the same path are merged.

Examples:
```
expand=user:firstName,email posts:title,createdAt posts.author:firstName
```


## Sorting

Space-separated list; prefix `-` for descending.
```
sort=-createdAt -publishedAt
```

When `after` is used, results preserve the expected chronological order.

## Pagination (cursor semantics)

- `after=<id>`: fetch items after the provided id (forward).
- `before=<id>`: fetch items before the provided id (backward).
- Default sort is newest first. Default `limit` is 20.
- Response shape:

```json
{
  "data": [
    { "id": "66ef0b3a2f1c0f0d9b3c1a22", "name": "John Doe", "email": "john@doe.com" }
  ],
  "metadata": { "hasMore": true, "totalCount": 128 }
}
```

`hasMore` is `true` when the page returns `limit` items. `totalCount` is only computed when requested via `countTotal`.

## End-to-end examples

### Filters
```
/customers?filter=email|eq|john@doe.com metadata.key|eq|value accountType|in|main,sub,virtual
/customers?filter=email:john@doe.com metadata.key:value -accountType:sub
/customers?filter=name:"John Doe" email~john
/customers?filter=name:<John Doe> email~john
/customers?filter=amount|gt|1000 amount|lt|2000
/customers?filter=amount>1000 amount<2000
/customers?filter=amount=2000 fees!=0
/customers?filter=createdAt|gtd|2020-01-01T00:00:00.000Z createdAt|ltd|2020-01-31T23:59:59.999Z
```

### Sorting, selecting, expanding
```
/logs?filter=method|eq|POST path|eq|/card-programs&select=path method initiator&countTotal=true
/logs?filter=method|eq|POST&select=path method initiator&countTotal
/entities?expand=user:firstName,email timeline.user:firstName

## Errors

Invalid filter format returns HTTP 400:

```json
{
  "statusCode": 400,
  "message": "Incorrect format for 'filter' parameter."
}
```
```

## Notes

- Values with spaces must be quoted: `name:"John Doe"` or `name:<John Doe>`.
- Some deeply nested `expand` paths may be truncated for performance; use `:` to choose fields per relation.
- For equality/not-equality, both `:` and `=`/`!=` are supported (e.g., `state:active`, `amount=2000`, `fees!=0`).