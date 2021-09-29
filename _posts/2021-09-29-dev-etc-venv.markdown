---
layout: post
title:  "[Python] venv"
subtitle:   "venv"
categories: dev
tags: dev etc   
comments: true
---


## Summary
> venv is a tool to create isolated Python environments.
  
- Index
    - [Create virtual environment](#Create-virtual-environment) 
    - [Activate virtual environment](#Activate-virtual-environment)
    - [Deactivate virtual environment](#Deactivate-virtual-environment)


## Create virtual environment
```bash
python -m venv .venv

echo '.venv' >> .gitignore
```


## Activate virtual environment
```bash
source .venv/bin/activate
```


## Deactivate virtual environment
```bash
deactivate
```
