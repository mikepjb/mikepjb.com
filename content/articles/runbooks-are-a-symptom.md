+++
title = 'Runbooks are a symptom'
date = 2025-02-01T00:07:07+01:00
draft = true
+++

Runbooks are bad UX.

Runbooks document how actions in your business should be performed. While they're a good first
step, for semi-frequent tasks we can do better. In web design, needing to explain your interface
suggests the design isn't clear enough. This reminds me of Mark Twain's quote: "I didn't have time
to write a short letter, so I wrote a long one instead."

A good progression from runbooks is creating a system that transforms these "long letters" into
"short ones" - making complex processes more straightforward and user-friendly.

## Enter the portal

An operations portal can effectively replace runbooks. This dedicated service allows you to
describe jobs in code, with structured configuration for different environments. Instead of
following manual steps, users interact with a purpose-built interface that guides them through the
process.

-- include a picture of a portal, jobs dashboard --

## Isn't this premature optimisation?

While runbooks help reload context for on-call engineers, they introduce inefficiency through
repetition. Each time someone follows a runbook, they're:
- Manually interpreting written instructions
- Context switching between documentation and execution
- Potentially introducing human error
- Spending time on mechanical tasks that could be automated

## This doesn't apply to me, my runbooks require manual steps

Even highly manual processes can benefit from partial automation. Consider a task requiring:
1. Logging into multiple dashboards
2. Copying information between systems
3. Verifying configurations
4. Making API calls

A portal can streamline these by:
- Providing direct links to relevant dashboards
- Pre-filling forms with known information
- Automating verification steps
- Handling API calls through a user-friendly interface

## Give it a go

Start small with your own portal. It doesn't need complex features like job queuing or extensive
configuration options. A single webpage with input fields can transform a runbook into a guided
process.

Ask yourself:
- Is there a part that can be hidden/calculated?
- Are there steps involving service connections or API requests that could be automated?

Here's a minimal starting point:

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <!-- HTMX provides dynamic updates without complex JavaScript -->
        <script src="https://unpkg.com/htmx.org@2.0.4" integrity="sha384-HGfztofotfshcF7+8n44JQL2oJmowVChPTg48S+jvZoztPfvwD79OC/LTtG6dMp+" crossorigin="anonymous"></script>
        <link rel="stylesheet" href="/style.css" type="text/css" media="all" />
    </head>
    <body>
        <!-- Real-time encoding with automatic updates -->
        <input type="text" 
               name="text" 
               hx-post="/encode"
               hx-trigger="keyup changed delay:200ms"
               hx-target="#result"
               placeholder="Enter text to encode">
        
        <div id="result"></div>
    </body>
</html>
```

Compare this to the equivalent runbook step:

```bash
# Manual encoding step requiring command line knowledge, how many times have you or someone else
# carefully Ctrl-b'd or held down the left arrow key until they are in the right place?
curl -X POST http://localhost:8080/encode \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -d "text=<enter your plaintext here>"
```

## Growing your portal

As you add more tasks, patterns emerge. Common operations like secret management or configuration
updates can become reusable components. For example:

1. Secret Management:
    - Create a reusable cipher component for handling sensitive data
    - Standardize encryption/decryption processes

2. Configuration Updates:
    - Automate pull request creation for config changes
    - Include validation and review workflows
    - Provide templated changes for common updates

By continuously identifying and abstracting common patterns, your portal evolves into a powerful
operations tool that makes complex tasks accessible and reliable.
