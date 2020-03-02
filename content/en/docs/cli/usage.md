---
title: "CLI Usage"
linkTitle: "CLI Usage"
weight: 20
description: Getting familiar with the Azurite CLI
---

The basic commands available are:

- Listing ships
  - By name: find ships by name
  - By class: list only ships from a specific class
  - By faction: list all the ships for a given faction
  - By type: list all the ships for a specific hull type (i.e. CA/CL/BB)
- Get details for a single ship
  - This includes all the details that we pull for a ship: names, details, equipment slots etc

Check the `--help` for each command to see all your options. Want to find all the Eagle Union CLs that can equip torps? Easy.

```bash
azurite list by-type CL --equip Torpedoes --faction "Eagle Union"
```
