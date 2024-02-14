---
date: <% moment(tp.file.creation_date()).format("YYYY-MM-DD")%>
week: <% moment(tp.file.creation_date()).weeks() %>
time:
  - task: "[[Dev Environment]]"
    time: 0 hours
    progress: 5
  - task: "[[Emails]]"
    time: 0 hours
    progress: 7
---
Date: <% moment(tp.file.creation_date()).format("dddd, MMMM DD, YYYY") %>
# Work Undertaken Summary


# Problems encountered and how you overcame them


# Time Spent
```dataview
TABLE WITHOUT ID
link(meta(entry.task.top-level-task).subpath) As "Top Level",
entry.task as "Second Level",
entry.time As "Time",
entry.progress as "Progress (%) this week est"
WHERE time != null
WHERE file = this.file
flatten time as entry
sort date desc
```

# Questions for Tutor


# Next work planned


# Raw Notes
<% tp.file.cursor() %>

