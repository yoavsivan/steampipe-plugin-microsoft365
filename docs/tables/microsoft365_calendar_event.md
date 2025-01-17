# Table: microsoft365_calendar_event

List previous and upcoming events scheduled in a specific calendar.

The `microsoft365_calendar_event` table can be used to query events from any calendar, if you have access; and **you must specify the user's ID or email** in the where or join clause (`where user_id=`, `join microsoft365_calendar_event on user_id=`).

## Examples

### Basic info

```sql
select
  subject,
  online_meeting_url,
  start_time,
  end_time
from
  microsoft365_calendar_event
where
  user_id = 'test@org.onmicrosoft.com'
order by start_time
limit 10;
```

### List upcoming events scheduled in next 4 days

```sql
select
  subject,
  online_meeting_url,
  start_time,
  end_time
from
  microsoft365_calendar_event
where
  user_id = 'test@org.onmicrosoft.com'
  and start_time >= current_date
  and end_time <= (current_date + interval '4 days')
order by start_time;
```

### List upcoming events scheduled in current month

```sql
select
  subject,
  online_meeting_url,
  start_time,
  end_time
from
  microsoft365_calendar_event
where
  user_id = 'test@org.onmicrosoft.com'
  and start_time >= date_trunc('month', current_date)
  and end_time <= date_trunc('month', current_date) + interval '1 month'
order by start_time;
```

### List events scheduled in current week

```sql
select
  subject,
  online_meeting_url,
  start_time,
  end_time
from
  microsoft365_calendar_event
where
  user_id = 'test@org.onmicrosoft.com'
  and start_time >= date_trunc('week', current_date)
  and end_time < (date_trunc('week', current_date) + interval '7 days')
order by start_time;
```
