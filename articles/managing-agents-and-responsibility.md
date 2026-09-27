---
layout: article
title: "Using Agents Responsibly for PR Lifecycle"
date: 2026-08-20
modifieddate: 2026-09-26
published: true
---

Here is a thought experiment for you: if you use agent to automate the Pull Request lifecycle - creating a PR, reviewing a PR, addressing conflicts, addressing comments, running pipelines to pass PR checks, even approving a PR - how do you understand what actualy happen and do you own the responsibility of mistakes made by agents?

This is already happening in an increasingly rate. I just started to leverage Github Copilot's Auto merge feature in the month of August 2026. This Auto merge feature can automatically create PR, address comments, fix CI failures, push for more fixes, and optionally even merge code. From the reviewer's perspective, they are also increasingly using AI agents to review codes.

As I check the vast amount of PR and PR comments handled by agent, I cannot stop but think we need to use agents more responsibly for PR lifecycle. We need to avoid the scenaior where nobody really knows what happen in the process, except they know that some PR with some requirements are created, and that PR is merged later.

There are places where automating PR lifecycle with agent is really helpful: for simple and mundane fixes that will neverthless be sit in backlog, AI agents can close this gap. However, when it is time to do critical feature implementation and fixes, this approach shifts the workload significantly to the later stage of PR: when reviewers have to decide approve and not approve, and when PR creators have to decide whether they should spend time to understand all the code and comments and what to do next.

I have looked at different PR managed by agents and found it difficult to follow. 1. PR description and comments are often very long and verbose. I need to be patient to sit through and read the comments. Most of these PR review comments made by AI are sound. The problem is they are not human friendly. 2. Reviewers don't understand the reviews made on behalf of them, and neither does the PR creator who relies on feature such as Auto merge to help them address genuine issues.

In fact this just happened to me. I have an automation in Github Copilot App to check active PR in the repo I maintain by following my instruction to provide new comments when there are new updates. This morning I just found that it even sliently approved one of the PRs, without my explicity consent. What happened is that this is a scheduled call of Copilot with the instruction I have as prompt and with the tools and MCP available in both my personal setting and repo. I never gave the agent explicity "github approve" tool, but this probably happened because I have chosn "allow all" when I set the automation, without realizing that this is one the tools I implicitely allowed. The good thing is that this is an internal only repo, and the PR is generally safe to be checked-in. After finding this out, I have edited the automation to prevent any actual approve action.  

Is there a better solution?

As I read about Andrej Karpathy's note on Agentic engineering, I totally agree with the most fundamental point in the new era: verifiability. If you can verify a thing, you can offload to agents. Connecting back to this PR lifecycle, if we can verify the work of agent review and comments, then we can "approve all".

To practice this, I did and will continue to do three things in the repo I managed:
1. I add a watermark for all the reviews and actions done by agent. I specified that in the Github Automation prompt that all actions start with **[Yuguang Automation]**, to clearly indicate to me and teammates that the actions are done on behalf of me.
2. Before choosing any auto-merge, I make conscious effort to decide if the PR risk level. Only low risks PR such as changing and updating README.md, POC testing codes that will not affect production usages can be auto-merged. For any other PR, never enable agent to merge the PR. Optionally if we can, we should enforce a new pipeline check, to enforce human consent to approve a PR, regardless of agent approve or not on behalf of user, and this step cannot be done by agent, such as leveraging something similar to Multi-factor authentication MFA for approving. When an agent approve a PR on behalf of the user, send a confirmation code to user, and have the user go back and type the code to signal human responsibility. Only when we can humanly verify the result should we allow "approve all".
3. Separate the test cases authoring from development and never have agents change critical test cases. If we allow agents to both write codes and test cases, agent will make the test cases to work for the codes. One reason for this is LLM is known to quickly wrap up results when it is near token limitation, so agents that depend on LLM to do the reasoning could come up with short cut to just make test cases work for the codes. If we need agents to write test cases, at least hand write enough critical test cases, or use a different model family.


These are for personal level to be a more responisble agent user. However, organization and team have to also do their own part to prevent misuse of agents.

For organization and team level, currently there is no way to guarantee if agents are used in a responsible way, until mistakes happen. This is a dangerous and a hidden issue for engineering team going forward as more and more companies push forward for agentic engineering. Teammates could act on good intention and be a responsible user of agents. In this case issues can be limited. But if there are organizational pressure, such as on delivery speed, and cultural pressure, then even responsbile engineers will be incentivized to chase for speed and let agents take over all the ciritical development and trust the results as-is without much due diligence and push to production and wait for Sev 2. We need to avoid the following sentences to occur:
- "I just let agents fix the bug / error for me, and the test pipeline succeeded, then I quickly checked the quality of a few test cases and they look good to me, so I just deployed to production. Production releases are also approved, so I assume it will be okay and because I have to work on another feature, let me swithc my attention there."
- "I just have my agents to run the evaluation for me for this prompt changes made by AI. I wrote some LLM-as-a-judge prompts, checked a few examples and they look good, then I completely trust the result of the LLM judges. When the eval result came back as improve over 10%, I am very happy and let agent to auto-merge the prompt changes"

I will share another article to talk about what I think should be in place to leverage the best of agents yet balance the risk.

This new way of working with AI Agent resembles how a manager is managing his or her team. I am not a people manager, but one big difference is trust. You built the trust with your team over some period of time, and you know someone is very reliable and someone is strong in which area. Only after this trust, can a manager be comfortable to offload almost all work to that teammate, and come back at the end to "approve a PR". If something did went wrong, responsibility is shared with that teammate. But with AI, they will just say "You're right. I am sorry...", and ultimately you as the AI manager take all the responsibility.