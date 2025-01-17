# Table: microsoft365_drive_file

List the specified user's drive items.

You must specify the user's ID or email in the where or join clause (`where user_id=`, `join microsoft365_drive_file on user_id=`).

## Examples

### Basic info

```sql
select
  name,
  id,
  path,
  created_date_time
from
  microsoft365_drive_file
where
  user_id = 'test@org.onmicrosoft.com';
```

### List all empty folders

```sql
select
  name,
  id,
  path,
  created_date_time
from
  microsoft365_drive_file
where
  user_id = 'test@org.onmicrosoft.com'
  and folder ->> 'childCount' = '0';
```

### List files modified after a specific date

```sql
select
  name,
  id,
  path,
  created_date_time
from
  microsoft365_drive_file
where
  user_id = 'test@org.onmicrosoft.com'
  and created_date_time > '2021-08-15T00:00:00+05:30';
```
