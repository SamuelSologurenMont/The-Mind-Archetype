# The-Mind-Archetype
The Mind Archetype — agent-native psychology experience powered by WebMCP.
# The Mind Archetype — Agent-Native Psychology with WebMCP

**The Mind Archetype** is an agent-native psychology experience that connects human visitors with AI agents through **WebMCP (Web Model Context Protocol)**.

The project demonstrates how a psychology website can expose structured, actionable capabilities to compatible AI agents while keeping professional decision-making and clinical responsibility with humans.

## 🚀 Live Demo

**Live website:**

https://themindarchetype.netlify.app/

The website is designed for both:

* 👤 Human visitors looking for psychological support
* 🤖 AI agents that need structured information and actions from the website

---

## 💡 What We Built

Traditional websites are primarily designed for humans to navigate through menus, pages, buttons, and forms.

The Mind Archetype adds an **agent-native interaction layer** using WebMCP.

Instead of forcing an AI agent to scrape or interpret the entire website, the site exposes structured tools that allow an agent to:

* Understand what The Mind Archetype is
* Explore services
* Identify relevant areas of care
* Understand the consultation process
* Answer common questions
* Access resources and books
* Prepare a consultation request
* Open contact options
* Provide the real appointment-booking experience

The goal is to transform a website from a passive information source into an **interactive capability layer for AI agents**.

---

# 🧠 WebMCP Implementation

The website registers WebMCP tools through the browser's WebMCP implementation using:

```javascript
document.modelContext
```

Compatible agents can discover the available capabilities through:

```javascript
await document.modelContext.getTools()
```

The current implementation exposes **12 WebMCP tools**.

## Available WebMCP Tools

| Tool                              | Purpose                                                           |
| --------------------------------- | ----------------------------------------------------------------- |
| `answer_common_question`          | Answers common questions about The Mind Archetype                 |
| `book_appointment`                | Provides the real Google Calendar appointment-booking experience  |
| `find_care_area`                  | Provides initial orientation based on a person's general concern  |
| `get_agent_demo_scenario`         | Provides a scenario for demonstrating the agent-native experience |
| `get_book_catalog`                | Returns the available book recommendations/catalog                |
| `get_care_process`                | Explains the consultation and care process                        |
| `get_first_consultation_guidance` | Provides guidance about the first consultation                    |
| `get_mind_archetype_profile`      | Returns structured information about The Mind Archetype           |
| `get_service_catalog`             | Returns the available services                                    |
| `open_contact_options`            | Provides available contact options                                |
| `prepare_consultation_request`    | Structures a person's consultation request                        |
| `search_mind_archetype_resources` | Searches available psychology resources                           |

---

# 📅 Agent-to-Action Example

One of the most important capabilities is `book_appointment`.

The agent does not invent appointment times or pretend to confirm a clinical appointment.

Instead, the WebMCP tool provides the actual Google Calendar booking page:

```text
https://calendar.app.google/cp8eicf9RJ4SAUjv6
```

The user then chooses an available time directly through Google Calendar.

This creates a clear boundary:

**AI → orientation and action**

**Human → clinical decision-making and appointment confirmation**

---

# 🔐 Human-Centered Safety

The project intentionally does **not** use the AI agent to diagnose mental health conditions.

The WebMCP layer is designed to:

1. Understand the person's general intention.
2. Provide structured orientation.
3. Explain available services.
4. Help identify the appropriate next step.
5. Prepare contact or consultation information.
6. Hand the person over to a human professional when clinical judgment is required.

The agent explicitly operates as an **orientation and navigation layer**, not as a replacement for professional psychological assessment.

---

# 👤 Human + Agent UX

The experience is designed around two complementary interfaces.

### Human experience

A person can:

* Explore the website normally
* Learn about psychological services
* Understand the consultation process
* Read resources
* Contact The Mind Archetype
* Book an appointment

### Agent experience

A compatible AI agent can:

* Discover the website's capabilities
* Query structured information
* Identify relevant services
* Guide a person toward an appropriate next step
* Prepare a consultation request
* Provide the actual booking action

The same website therefore becomes useful to both humans and AI agents without requiring a separate AI application.

---

# 🧪 How to Test WebMCP

## Chrome

Use a recent version of Chrome with WebMCP support enabled.

For testing, open:

```text
chrome://flags
```

Enable:

```text
WebMCP for testing
```

Then relaunch Chrome.

---

## Discover the Tools

Open the live website:

https://themindarchetype.netlify.app/

Then open:

```text
DevTools → Console
```

Run:

```javascript
(await document.modelContext.getTools()).map(t => t.name)
```

The expected result is an array containing the 12 WebMCP tools:

```text
[
  "answer_common_question",
  "book_appointment",
  "find_care_area",
  "get_agent_demo_scenario",
  "get_book_catalog",
  "get_care_process",
  "get_first_consultation_guidance",
  "get_mind_archetype_profile",
  "get_service_catalog",
  "open_contact_options",
  "prepare_consultation_request",
  "search_mind_archetype_resources"
]
```

---

# 🔎 Test a WebMCP Tool

For example, retrieve the structured profile of The Mind Archetype:

```javascript
const tool = (await document.modelContext.getTools())
  .find(t => t.name === "get_mind_archetype_profile");

await document.modelContext.executeTool(
  tool,
  JSON.stringify({language:"es"})
)
```

The tool returns structured information that an agent can use without parsing the visual website.

---

# 📅 Test Appointment Booking

Run:

```javascript
const tool = (await document.modelContext.getTools())
  .find(t => t.name === "book_appointment");

await document.modelContext.executeTool(
  tool,
  JSON.stringify({modality:"online"})
)
```

The result includes the real Google Calendar booking URL:

```text
https://calendar.app.google/cp8eicf9RJ4SAUjv6
```

The tool does not fabricate availability or create a fake appointment confirmation.

---

# 🏗️ Architecture

The project uses a simple agent-native architecture:

```text
                 ┌──────────────────────┐
                 │     Human Visitor    │
                 └──────────┬───────────┘
                            │
                            ▼
                 ┌──────────────────────┐
                 │  The Mind Archetype  │
                 │      Website         │
                 └──────────┬───────────┘
                            │
             ┌──────────────┴──────────────┐
             │                             │
             ▼                             ▼
     Human UI / UX                  WebMCP Tool Layer
                                           │
                                           ▼
                                  ┌─────────────────┐
                                  │    AI Agent     │
                                  └────────┬────────┘
                                           │
                           ┌───────────────┼───────────────┐
                           ▼               ▼               ▼
                       Orientation      Resources      Actions
                           │                               │
                           ▼                               ▼
                    Human professional          Google Calendar /
                    when appropriate             Contact flow
```

---

# 🌎 Why WebMCP Matters

Mental-health websites often contain large amounts of information, but finding the correct next step can still require significant navigation.

WebMCP creates another interaction model:

> **Instead of asking an AI agent to understand the entire website, the website can explicitly tell the agent what it can do.**

This makes the experience:

* More structured
* More reliable
* More actionable
* Easier for agents to interact with
* Easier to connect to real-world actions

For The Mind Archetype, this means an AI agent can help turn a person's initial intention into a clear next step without attempting to replace the psychologist.

---

# 🎯 Potential Impact

The architecture can extend beyond one psychology practice.

The same pattern could be used by:

* Mental-health clinics
* Healthcare organizations
* Educational institutions
* Professional service businesses
* Wellness platforms
* Organizations offering human-centered support

A website can expose its capabilities directly to agents while preserving the existing human experience.

This creates a path toward **agent-native services without requiring organizations to rebuild their websites as AI applications.**

---

# 🛠️ Technology

* HTML
* CSS
* JavaScript
* WebMCP
* Chrome WebMCP testing environment
* Google Calendar
* Netlify

No separate AI backend is required for the core WebMCP interaction layer.

---

# 👨‍⚕️ About The Mind Archetype

**The Mind Archetype** is a psychology brand founded and directed by **Samuel Sologuren**, psychologist and clinical professional.

The project combines psychological services, educational resources, human-centered care, and emerging agent-native web technology.

The core principle behind the WebMCP implementation is simple:

**AI can help people navigate information and take the next step, while clinical judgment remains with qualified professionals.**

---

# 📜 License

This project is released under the **MIT License**.

See the [`LICENSE`](./LICENSE) file for the complete license text.

---

# 🏆 Built for the WebMCP Challenge

This project was created for the **OpenAI WebMCP Challenge** to explore how WebMCP can transform traditional websites into experiences that are discoverable and actionable by AI agents.

The project focuses on:

* WebMCP tool discovery
* Structured agent interaction
* Human + agent UX
* Safe handoff to human professionals
* Real-world actions
* Agent-native web architecture

**The website is not just readable by agents — it is usable by agents.**
