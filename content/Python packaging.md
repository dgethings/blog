---
title: Python Packaging
description: The state of Python packaging
draft: false
tags:
  - python
  - packaging
date: 2024-10-20
---
When starting out with Python it's pretty simple, you just need a Python interpreter, whatever libs you need and a text file containing the Python code doing what you want.

But once you get to the stage where you want to share that script with others you enter the messy world of Python packaging. It's a little surprising this situation is as it is given how long Python has been in use.

The [Python Enhancement Proposal](https://peps.python.org/) body has been gradually approving PEPs to address this area there still is plenty of work to do. There are a few projects implementing these PEPs and sometimes extending what is currently agreed. Projects like [uv](https://docs.astral.sh/uv/) and [PDM](https://pdm-project.org/en/latest/) are prime examples.

There is also the [torero](https://www.itential.com/blog/torero/introducing-torero-the-automation-gateway-you-didnt-know-you-needed/) product. This product doesn't just package Python scripts other things like [[Ansible]] too.