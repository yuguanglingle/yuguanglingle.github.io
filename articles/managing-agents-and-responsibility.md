---
layout: article
title: "Managing Agents and Responsibility"
date: 2026-08-20
published: true
---

Here is a thought experiment for you: if you use agent to automate the Pull Request lifecycle - creating a PR, reviewing a PR, addressing conflicts, addressing comments, running pipelines to pass PR checks, even approving a PR - how do you understand what actualy happen and do you own the responsibility of mistakes made by agents?

This is going to happen very soon, as I have just started to leverage Github Copilot's Auto merge feature. This Auto merge feature can automatically create PR, address comments, fix CI failures, push for more fixes, and optionally even merge code. From the reviewer's perspective, they are also increasingly using AI agents to review codes.

What this means in practice is nobody really knows what happen in the process, except they know that some PR with some requirements are created, and PR is merged later.

I have looked at different PR managed by agents and found it difficult to follow. 1. PR description and comments are often very long and verbose. I need to be patient to sit through and read the comments. Most of these PR review comments made by AI are sound. The problem is they are not human friendly. 2. Reviewers don't understand the reviews made on behalf of them, and neither does the PR creator who relies on feature such as Auto merge to help them address genuine issues.

There are places where this is really helpful: for simple and mundane fixes that will neverthless be sit in backlog, AI agents can close this gap. However, when it is time to do critical feature implementation and fixes, this approach shifts the workload significantly to the later stage of PR: when reviewers have to decide approve and not approve, and when PR creators have to decide whether they should spend time to understand all the code and comments and what to do next.

Is there a better solution?

A slight tangent to our train of thougts, this new way of working with AI Agent resembles how a manager is managing his or her team. I am not a people manager, so I cannot say for sure, but one big difference is trust. You built the trust with your team over some period of time, and you know someone is very reliable and someone is strong in which area. Only after this trust, can a manager be comfortable to offload almost all work to that teammate, and come back at the end to "approve a PR". If something did went wrong, responsibility is shared with that teammate. But with AI, they will just say "You're right. I am sorry...", and ultimately you as the AI manager take all the responsibility.

Is there a better solution without going back to the old days of manually manage the PR lifecycle? Solutions or mitigations here could also be helpful to other tasks that are increasingly being automated by AI.

Stay tuned as I explore these mitigations