---
title: "{{ replace .File.ContentBaseName "-" " " | title }}"
date: {{ now.UTC.Format "2006-01-02T15:04:05Z" }}
publish: false
---
