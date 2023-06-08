# Atlas slow command poc

Atlasgo has a performance issue with the lint / migrate command relate

if you run `atlas migrate lint --latest 1 --dev-url docker://mysql/8/dev` it will take minutes to resolve.

the issue is related to a mysql query to get tables / foreign key and mysql is stuck in `checking permissions; for a long time


```
#show processlist

| Id | User            | Host             | db   | Command | Time | State                  | Info
| 10 | root            | 172.17.0.1:54140 | dev  | Execute |   29 | checking permissions   | SELECT
	t1.CONSTRAINT_NAME,
	t1.TABLE_NAME,
	t1.COLUMN_NAME,
	t1.TABLE_SCHEMA,
	t1.REFERENCED_TABLE_ |
