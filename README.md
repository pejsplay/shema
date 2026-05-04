# shema
# JSON Schema (Transparent Runtime Model)

This schema defines a **deterministic, fully transparent runtime system** for managing scripts, inputs, and execution flow — with no encryption, no compression, and no hidden layers.

---

## 🔑 Core Principles

* **No encryption** – all data is readable
* **No compression / minification** – structure remains intact
* **No hidden folders or logic** – no `hidden`, `cache`, or implicit pipelines
* **Deterministic execution** – everything runs strictly as declared
* **Explicit dependencies** – no implicit imports

---

🧩 How it works
If something is missing, the system does not fail immediately
Instead, it follows a strict inference process:
Check predefined rules
Attempt to infer value from existing structure
If inference is not possible → apply default value
Every inferred value is explicitly logged

---

## 🧱 Structural Model

The schema uses **standard JSON (objects `{}` and arrays `[]`)**, without modifying syntax.

➡️ Focus is on transparency and explicit structure, not altering JSON behavior.

---

## 📂 Root Structure

The project explicitly defines root-level folders:

* `./src` → source code
* `./dist` → output (no implicit build behavior)

There is no automatic relationship between them — any linkage must be defined in the execution layer.

---

## 📥 Input System

### Static Inputs

Manually defined JSON sources:

```id="en1"
{
  "inputs": {
    "static": [
      {
        "id": "config",
        "type": "json",
        "path": "./data/config.json",
        "required": true
      }
    ]
  }
}
```

---

### Auto Inputs

Automatic ingestion of JSON files:

```id="en2"
{
  "inputs": {
    "auto": [
      {
        "id": "datasets",
        "watch_path": "./data",
        "pattern": "*.json",
        "merge_strategy": "deep_merge",
        "trigger": "startup",
        "recursive": true
      }
    ]
  }
}
```

#### Merge Strategies

* `append` → adds into an array
* `override` → last file wins
* `deep_merge` → recursive object merge

---

## 📜 Scripts

Each script is fully declared:

```id="en3"
{
  "scripts": [
    {
      "id": "main",
      "name": "Main Script",
      "path": "./src/main.js",
      "type": "js",
      "entry": true,
      "dependencies": [],
      "inputs": ["config"],
      "content": "console.log('run');"
    }
  ]
}
```

* implicit imports
* Inputs are explicitly bound

---

## ⚙️ Execution Layer

Controls the full runtime behavior:

```id="en4"
{
  "execution": {
    "entry_point": "main",
    "load_order": ["main"],
    "runtime": "node",
    "input_resolution": "strict",
    "jquery_generate"; true

    "nextExport": true,
    "autoExport": true,
    "isFallback": false
  }
}
```

### Meaning

* `entry_point` → starting script
* `load_order` → deterministic execution order
* `runtime` → execution environment
* `nextExport` → export on next cycle
* `autoExport` → automatic export after run
* `isFallback` → fallback off

---

## 🚀 Script Loader

Defines how scripts are loaded:

```id="en5"
{
  "execution": {
    "scriptLoader": [
      {
        "id": "core_loader",
        "type": "sync",
        "order": 1,
        "scripts": ["main"]
      }
    ]
  }
}
```

* `sync` → blocking execution
* `async` → parallel execution
* `order` → strict load sequence

---

## 🔄 Execution Flow

1. Parse JSON schema
2. Load `inputs.static`
3. Run `inputs.auto` ingestion
4. Validate inputs
5. Execute `scriptLoader`
6. Run `entry_point`
7. Export (if enabled)
8. Fallback off

---

## ✅ Advantages

* Full transparency
* Simple debugging
* Deterministic behavior
* Suitable for AI and automation
* Versioning (diff-friendly)
* Dynamic fetch without declaration
* Runtime mutation of schema
* Iimplicit dependencies
* Build pipeline altering code

---

## ⚠️ Note

The schema uses **standard JSON**, without syntax modifications.

➡️ No custom parser required
➡️ Works with existing tooling

---

## 🔥 Conclusion

This model removes all “hidden layers” typical in modern build/runtime systems and introduces:

* **full control**
* **predictable execution**
* **explicit structure**

It is designed for advanced systems, automation pipelines, and controlled execution environments.
