---
tags: 
description: The stages of network automation maturity and how to recognise them
title: Stages of Network Automation Maturity
---
It can be hard to know where you are in the world of [[Network Automation]]. This is especially difficult without a clear view of what the end goal is.

In this article I will define what I see are the stages of [[Network Automation]] maturity. They are generalisations that will hold mostly true. They should be recognisable even if they do not match exactly with your situation.
# Reduction of Toil
This is the typical starting point. There is some task or action that is repetitive, laborious or tedious but also trivial enough that someone thinks "I could script this". So they do.

At this stage there is little to no coordination of who or what tools are developed, or in what language. It's just freeform development of "low hanging fruit" problems that is a quality of life improvement for the engineer.

The user of tool is the author and geared around a technology that person knows or wants to learn about. Usually this is [[Python]] or [[Ansible]].

The tool is an encoding of knowledge. Information about inventory (i.e. devices that the tool run against) is separated from the tool. Such as an [[Ansible Inventory]] or a command line argument for a [[Python]] script.

The output of the tools is designed to be read by the user or possibly copied into another tool like [[Excel]]. If a tool like [[Ansible]] is used then the output is either the usual playbook output or a text file.
# Tools as a Service
Now there is a collection of useful tools the obvious next step is increase the audience of users. The main business value is time saved and how that can be magnified to a wider audience.

This stage builds on the [[#Reduction of Toil]] by adding coordination to the tools produced. A big part of this stage is standardisation, on language, inputs and outputs and there are more users than developers. Tools that have overlapping functionality are consolidated.

The purpose of the standardisation to ease sharing of the tools and minimise learning of how to use the tools. This standardisation also has benefits in how the tools are distributed to users.

A lot of thought and time can be wasted working out how best to make these tools discoverable so people don't continue to develop their own and use what exists already.
# Service Integration
At this stage you have mostly solved tool discovery and people are forming well defined patterns of operation. You are now thinking in terms of automating multistage processes that are usually documented on a wiki or a collection of documents.

In this context "services" means things like green field or brown field deployments, OS upgrades - including pre and post checks, RMAs, things like that. Any activity you would normally perform to maintain a functioning network. The development of these services are for users that will never be developers of these services.

Services are be created with a specific class of user in mind: Deployment, Operations, Engineering, etc. You have, or form, a mechanism to share the services with these user classes. Along with the creation of these services you will create user guides, training sessions and support models.

Inventory providence, accuracy and integrity will naturally become important at this stage, if not already. If not already the inventory will begin to move from [YAML](https://yaml.org/) or [[Excel]] files.
# Service Orchestration
At this stage the use of automated services are so well established that people begin to question the sense of human initiation and termination of these services. By this I mean people question does i makes sense for a human at 2am to kick off an automated upgrade and then manually close the ticket at 3am once the automation is complete.

Carrying on the upgrade example. Service Orchestration is about Engineering qualifying a new version of an OS. Once done this automatically triggering a process that identifies all the network devices that need upgrading, scheduling those upgrades in accordance to policy (rarely do you want the automated system to upgrade all affected devices just because it could). Human responsibility is focussed on refining and managing the automated service, not nannying it.

To achieve this level services orchestration requires trusted, high quality, centralised inventory repositories. Both the data and processes need to be human and machine readable. Both parties need to be able to reason about how the service is - or will be - orchestrated. Virtually all execution is automated meaning people need to not only trust but verify that the automation cannot fail in unrecoverable and catastrophic ways.

These inventories are better known as a [[Source of Truth]] or [[Network Source of Truth]]. There are a lot of decisions about how to best build them. These decisions are both technical and organisational. Once you have built a [[Source of Truth]] the main challenge is keeping the data it stores as accurate and relevant as possible.

If not done already you have made the realisation that the intended state of the network is not the network itself but is in you network management stack. From this point on the production network is seen as an instance of that intented state.
# Network Orchestration
This stage is about maturing the automation such that everything is done via service orchestration. That only the most novel or tricky of situations require human intervention and there is a way to integrate these new things into an automated workflow.

You can expose these services to other Infrastructure teams such that they can treat the network as a [PaaS](https://en.wikipedia.org/wiki/Platform_as_a_service), or in house [NaaS](https://en.wikipedia.org/wiki/Network_as_a_service). This stage can also be viewed as [Intent Based Networking](https://datatracker.ietf.org/doc/rfc9315/).
# Infrastructure Orchestration
This is the final stage. Here pilars of Infrastructure are integrated such that it is fully business aligned. For example at this stage you use automation to fully - and accurately - predict the costs and lead time to business questions such as "how long and how much will it cost to build an AI model to X".

While there are still separate teams that manage networking, compute and storage, the alignment of these teams is very strong. This means that application owners can describe the resources their application needs and the [PaaS](https://en.wikipedia.org/wiki/Platform_as_a_service) automatically creates and manages the infrastructure needed.



