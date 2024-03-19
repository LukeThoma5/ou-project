---
date: <% moment(tp.file.creation_date()).format("YYYY-MM-DD")%>
week: <% moment(tp.file.creation_date()).weeks() %>
draft: true
---
Date: <% moment(tp.file.creation_date()).format("dddd, MMMM DD, YYYY") %>
# Work Undertaken Summary


# Risks


# Time Spent


# Questions for Tutor


# Next work planned


# Raw Notes
<% tp.file.cursor() %>

