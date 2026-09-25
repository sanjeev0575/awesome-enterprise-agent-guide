# awesome-enterprise-agent-guide

# Awesome Enterprise Agent Guide

This repository is a 10-day learning series about building an AI agent from absolute zero to a production-ready system. It shows how to design, build, test, deploy, secure, govern, and observe an AI agent using Gemini Enterprise Agent Platform.

The series uses one project throughout: a Kubernetes Incident Investigator. Each day adds one important part of the agent lifecycle, starting with a simple prototype and ending with a complete production architecture.

## What this series covers

### Day 1: Why prototypes fail in production
- Understand the difference between a working demo and a production-ready agent.
- See how a Kubernetes troubleshooting agent can give the wrong answer when it only looks at logs.
- Learn why a single successful incident does not prove reliability.
- Understand the real production questions:
  - Can we trust the agent’s answers?
  - Where will it run?
  - Can it remember previous incidents?
  - Who is this agent?
  - What is it allowed to access?
  - Can we see what it did?
  - What does it cost to run?
  - Who is accountable for it?
- Learn what it means to move from Day 1, a prototype, to Day 2, a real system that can operate inside an organization.

### Day 2: Build your first AI agent with ADK
- Start the Kubernetes Incident Investigator project from an empty repository.
- Learn how ADK turns a model, instructions, and tools into an agent.
- Build the first version of the agent in a local development environment.
- Define the agent’s job clearly:
  - Investigate a Kubernetes incident.
  - Explain the likely root cause.
  - Always list the evidence used.
- Manually provide logs and events to the agent and watch how it reasons.
- See that the agent can give useful answers when evidence is provided.
- Learn its first limitation: it cannot collect evidence on its own yet.

### Day 3: Give the agent tools to investigate Kubernetes
- Learn why an agent should collect evidence instead of guessing.
- Add tools that let the agent:
  - Check workload status
  - Read Kubernetes events
  - Fetch logs
  - Inspect recent deployments
- Add tools one at a time and see how each one improves the investigation.
- Teach the agent an investigation procedure so it follows a sensible order.
- Make sure it checks recent changes before concluding.
- Break a service and watch the agent investigate on its own.
- Understand the remaining shortcut: it still reaches the cluster using credentials from the local machine.

### Day 4: Evaluate the agent before trusting it
- See why one correct incident is not enough.
- Build an evaluation set of incidents with known answers.
- Include cases such as:
  - A pod that keeps restarting
  - A missing configuration
  - A failed database connection
  - A deployment that introduced a problem
- Test the agent against every case.
- Measure both:
  - Whether it found the correct root cause
  - Whether it investigated in a sensible way
- Improve the agent based on evaluation failures.
- Re-run the evaluation until it passes.
- Learn how to use evaluation as a repeatable test every time the agent changes.

### Day 5: Deploy the agent to Google Cloud with Agent Runtime
- Move the agent from the local machine to Google Cloud.
- Learn why a real agent needs a reliable place to run.
- Understand what Agent Runtime provides:
  - Managed execution
  - Scaling
  - Multiple conversations at once
  - Conversation history
- Deploy the same local agent without changing its design.
- Put a simple interface in front of it so the team can use it.
- See that development still happens locally, while Google Cloud becomes the production runtime.
- Understand the tradeoff: the agent is given broad read access for speed, and that will need to be improved later.

### Day 6: Give the agent long-term memory with Memory Bank
- Learn why memory matters when an agent works with a team over time.
- Understand the difference between:
  - Conversation history, which lasts for one conversation
  - Long-term memory, which lasts across conversations and users
- Save useful incident summaries after investigations end.
- Store:
  - Symptoms
  - Root cause
  - Fix
- Search previous incidents when a new investigation starts.
- Use past experience as a starting point without blindly repeating old conclusions.
- Add an evaluation case where similar symptoms lead to a different cause.
- Learn that memory should support investigation, not replace verification.

### Day 7: Give the agent its own identity with SPIFFE
- Understand why shared credentials are a problem.
- Learn how audit logs become unclear when many systems use the same service account.
- See how a SPIFFE ID gives the agent a verifiable identity.
- Give the agent its own identity for accessing the cluster.
- Remove copied credentials.
- Configure the cluster to trust the agent’s identity for read-only access.
- Re-run evaluation to confirm nothing broke.
- Compare audit logs before and after to see exactly which agent made each request.

### Day 8: Control what the agent can access with Agent Gateway
- Learn why identity alone is not enough.
- See why dangerous actions like restarting deployments should not be left to the agent.
- Understand the principle of least privilege.
- Define what the Kubernetes Incident Investigator should be allowed to do:
  - Read workloads
  - Read events
  - Read logs
  - Read deployment information
- Define what it should not be allowed to do:
  - Delete pods
  - Restart applications
  - Change configuration
  - Read secrets
- Route tool calls through Agent Gateway.
- Enforce policy outside the agent’s own code.
- Watch the agent get denied when it asks to restart a service or read a secret.
- Learn how the agent should respond by telling a human what to do instead.

### Day 9: Monitor, govern, and control cost
- Learn how to operate an AI agent like a production application.
- Add tracing for every investigation.
- See each:
  - Model call
  - Tool call
  - Step duration
- Combine traces, logs, gateway events, and audit entries into one view.
- Add cost awareness by tracking:
  - Model tokens
  - Tool calls
  - Investigation usage
- Set alerts for unusually expensive investigations.
- Define governance:
  - Who owns the agent
  - What it can do
  - What it can remember
  - Who reviews changes
- Turn production failures into new evaluation cases.
- Learn how monitoring and evaluation work together.

### Day 10: From prototype to production
- Bring together everything built across the series.
- Revisit the original prototype and the questions it could not answer.
- Run a real incident through the complete system.
- Confirm the agent can now:
  - Be trusted through evaluation
  - Run on Agent Runtime in Google Cloud
  - Remember past incidents with Memory Bank
  - Prove its identity with SPIFFE
  - Stay within access limits through Agent Gateway
  - Be observed end to end through tracing and logs
  - Be measured for cost
  - Be owned and governed clearly
- Understand how each capability was added because of a real production need.
- See the final result: a Kubernetes Incident Investigator that is ready for a real organization.

## Series goal

The goal of this repository is to help learners understand how to move from a simple AI agent prototype to a system that can run safely in a real organization.

## Main project idea

The central example throughout the series is a Kubernetes Incident Investigator. The agent helps investigate incidents by checking logs, events, recent changes, memory, identity, permissions, and traces before drawing a conclusion.

## Tech stack

- Gemini Enterprise Agent Platform
- Agent Development Kit
- Google Cloud
- Kubernetes

## How to use this repository

Use this repository as the home for the full 10-day learning series. Each day explains one part of the journey from prototype to production.

## License

Add a license before publishing if needed.
