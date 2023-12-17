In the context of [[PostgreSQL]], a popular open-source relational database, there are two types of indexes that can speed up full-text searches: GIN (Generalized Inverted Index) and GiST (Generalized Search Tree) [1](https://www.postgresql.org/docs/9.1/textsearch-indexes.html).

A GiST-based [[Index]] can be created with the following SQL command:

```sql
CREATE INDEX name ON table USING gist(column);
```

The column can be of `tsvector` or `tsquery` type. However, GiST indexes are lossy, meaning that the index may produce false matches, necessitating a check of the actual table row to eliminate such false matches [1](https://www.postgresql.org/docs/9.1/textsearch-indexes.html).

A GIN-based index can be created with the following SQL command:

```sql
CREATE INDEX name ON table USING gin(column);
```

The column must be of `tsvector` type. GIN indexes are not lossy for standard queries, but their performance depends logarithmically on the number of unique words [1](https://www.postgresql.org/docs/9.1/textsearch-indexes.html).

The choice between GiST and GIN depends on various factors:

- GIN index lookups are about three times faster than GiST.
- GIN indexes take about three times longer to build than GiST.
- GIN indexes are moderately slower to update than GiST indexes, but about 10 times slower if fast-update support was disabled.
- GIN indexes are two-to-three times larger than GiST indexes.

As a rule of thumb, GIN indexes are best for static data because lookups are faster. For dynamic data, GiST indexes are faster to update [1](https://www.postgresql.org/docs/9.1/textsearch-indexes.html).

PostgreSQL's full-text search capabilities can be leveraged using the `@@` operator, as shown in this example:

```sql
SELECT to_tsvector('fat cats ate fat rats') @@ to_tsquery('fat & rat');
```

This will return true if the document (in this case 'fat cats ate fat rats') contains both 'fat' and 'rat' [4](https://www.garysieling.com/blog/gin-vs-gist-for-faceted-search-with-postgres-full-text-indexes/).