# Статья

* [Deep dive into PostgreSQL internal statistics. Алексей Лесовский](https://pcnews.ru/top/blogs/2day/deep_dive_into_postgresql_internal_statistics_aleksej_lesovskij-989389.html#gsc.tab=0)

## DB

```a
SELECT * FROM pg_stat_database where datname = 'test' \gx
```

### На что обратить внимание

blks_read
blks_hit

#### % попадания в кэш (чем выше тем лучше, но не меньше 90%)
Она позволяет оценить, какой объем данных берется из кэша shared buffers, а какой объем читается с диска.

```s
select
sum(blks_hit)*100/sum(blks_hit+blks_read) as hit_ratio
from pg_stat_database;
```

