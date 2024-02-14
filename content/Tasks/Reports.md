# Total Time Spent
```dataview
TABLE WITHOUT ID Task As Task, sum(rows.entry.time) As "Total Hours"
WHERE time != null
flatten time as entry
group by entry.task as Task
```

# Time Spent By Major Task
```dataview
TABLE WITHOUT ID Task As Task, sum(rows.entry.time) As "Total Hours"
WHERE time != null
flatten time as entry
group by link(meta(entry.task).path) as Task
```

# Time Spent with breakout

```dataview
TABLE WITHOUT ID
link(meta(Task.top-level-task).subpath) As "Top Level",
Task as "Second Level", sum(rows.entry.time) As "Total Hours",
Task.estimate As "Estimate",
choice(!Task.original-estimate, Task.estimate, Task.original-estimate) as "Original Estimate",
((sum(rows.entry.time.minutes) / Task.estimate.minutes) * 100) as "Percent Time Used",
sum(rows.entry.progress) as "Percent Complete (Est)"
WHERE time != null
flatten time as entry
group by entry.task as Task
```


# Time Sheet
```dataview
TABLE WITHOUT ID date as Date, 
link(meta(entry.task.top-level-task).subpath) As "Top Level", entry.task as "Second Level",
file.link as Card,
entry.time As "Time"
WHERE time != null
flatten time as entry
sort date desc
```
