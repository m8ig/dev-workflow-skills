---
name: set priorities straight
description: "Read this first before any development task. Defines the priority hierarchy of rules: skills override defaults, AGENTS.md overrides skills, user instructions override everything."
---

All rules and requirements are set on different levels. The skills that you can use to create or generate basic things:

1. How to choose the technical stack of a project
2. How to create a new repo / library / component
3. Some basic principles of how to work with styles
4. Different features, services, and actions

All of that is loaded in the root `CLAUDE.md` file from the Obsidian vault and LLM skills folder.

The next level is the `AGENTS.md` file in the root of the specific project folder. Here I describe some basic things regarding this specific project. If any statements in the file contradict previous skills, then you should choose them as a priority, because project-specific rules can override general rules.

After that, we have a `AGENTS.md` file in each app folder. In the case of mono-repo, we can have from 2 to 5 different apps: API, web, landing, mobile, etc. Those rules have priority regarding the specific project they are placed in. So if you see any updated rules inside the web app folder, it means that those rules are applied only to the web app.

The final level — `AGENTS.md` file inside each library folder. Since I'm using mostly the nx approach for architecture, all functionality of different apps is divided into different libraries. And those libraries are grouped by the name of the feature they belong to. Please check `Create a new feature library.md` skill for more information. Those files can contain only the product description of how the feature works, so you can implement it completely in all the different apps at the same time.
