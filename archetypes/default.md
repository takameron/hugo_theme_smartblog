---
title: "{{ replace .Name "-" " " | title }}"
date: {{ .Date }}
lastmod: {{ .Date }}
author: "{{ .Site.Params.author.name }}"
images: ["post-cover.png"]
categories: ["category1"]
tags: ["tag1","tag2"]
archives: ["{{ dateFormat "2006" .Date }}","{{ dateFormat "2006-01" .Date }}"]
toc: true
draft: true
---
