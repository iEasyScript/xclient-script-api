<p align="center">
  <img src="https://raw.githubusercontent.com/iEasyScript/xclient-script-template/main/.github/crest.png" width="120" alt="Project X">
</p>

<h1 align="center">Project X Script API</h1>

<p align="center">
  The API Old School RuneScape scripts are written against, in Java.<br>
  <a href="https://ieasyscript.github.io/xclient-script-api/"><b>Browse the API reference</b></a> ·
  <a href="https://xclient.dev/osrs/developer/docs">Developer docs</a> ·
  <a href="https://github.com/iEasyScript/xclient-script-template">Script template</a>
</p>

---

**[The API reference](https://ieasyscript.github.io/xclient-script-api/)** lists every class, method and field
a script can use, with its documentation, and is searchable (press **/**). It is generated from the client's own
source and rebuilt for every client release; the footer of each page says which one.

Scripts are RuneLite plugins compiled against the [Project X client](https://xclient.dev). Almost everything a
script needs comes from one import, which gives short names like `Inventory`, `Bank`, `Walker`, `Objects` and
`Npcs`:

```java
import net.runelite.client.plugins.projectx.bot.*;

SceneObject rock = Objects.query("Copper rocks").nearestReachable();
if (rock != null) {
    rock.interact("Mine");
}

Npcs.query("Cow").interact("Attack");

if (Inventory.isFull()) {
    Bank.depositAll();
}
```

## What is in the reference

| Package | What it holds |
|---|---|
| `net.runelite.client.plugins.projectx` | `Script`, the base of every script, and `ProjectX`, the shared helpers and status line |
| `net.runelite.client.plugins.projectx.bot` | The action API: `Objects`, `Npcs`, `GroundItems`, `Players`, `Inventory`, `Bank`, `Walker`, `Widgets`, `Dialogue`, `Prayers`, `Magic` and more |
| `net.runelite.client.plugins.projectx.statemachine` | `StateMachineScript`, for scripts with three or more phases |
| `net.runelite.client.plugins.projectx.util.reliability` | Guarded steps, preconditions, checkpoints and recovery |
| `net.runelite.client.plugins.projectx.util.overlay` | `ScriptPanel` and `SkillTracker`, the stats panel every store script shows |
| `net.runelite.client.plugins.projectx.inventorysetups` | Saved inventory setups, loaded with `Loadout` |
| `net.runelite.client.plugins.projectx.breakhandler` | Taking breaks: `BreakHandlerScript` |

Everything else in the client is internal and can change between releases without notice.

## Where to start

1. Clone the **[script template](https://github.com/iEasyScript/xclient-script-template)**: a complete, small
   script that builds in one command, with the stats panel, an inventory setup picker and a state-machine loop.
   It downloads the client jar to compile against, so you only need a JDK 11.
2. Read the **[developer docs](https://xclient.dev/osrs/developer/docs)**: the guide from an empty project to a
   published script, an API cookbook, and the threading rules that matter.
3. Keep **[the reference](https://ieasyscript.github.io/xclient-script-api/)** open while you write.
4. Submit your script on the **[developer portal](https://xclient.dev/osrs/developer)**. Every build is reviewed
   before it goes live, and you set your own price in X Tokens.

## Versions

Two numbers matter, and the reference names both at the bottom of every page:

| | What it is | Where it goes |
|---|---|---|
| **Client release** | What the client is called (`2.12.0`) | `projectxClientVersion` in the template's `gradle.properties` |
| **Plugin API** | What the client offers scripts (`3.0.1`) | `minClientVersion` in your `@PluginDescriptor` |

Always build against the client players are running: item, object and widget ids are compiled into your classes,
so a jar built against an old client keeps old values after a game update.
