---
tags: 
title: Validating Network Designs
description: How to use BDD to validate your network design
draft: true
aliases: 
date: 2024-10-06
---
How to do testing coverage like code coverage but for network configurations.
Use Gherkin, BDD, to define the behaviour of your network design
If using Python I recommend behave over pytest.bdd, for it more consistent output
Think of the config as a collection of "features", SNMP is a feature, local auth is a feature, 8021.X on the edge is a feature. Create at lease one feature file for each of those features and then think of all the ways you use that "feature". For each way create a scenario
Things get a little more complicated with the Steps. Not that Steps are inherently complex, but you are trying to do 2 things at once with them:
1. Define a specific step
2. Make modular reusable steps to aid maintenance 
Don't try to do both of these at the same time when creating a step. Just create the step as it makes sense at the time. Once you've created all the steps for all of the scenarios then you can review the steps to make them modular