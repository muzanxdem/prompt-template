# Prompt templates for RAG benchmark

This directory holds `.txt` prompt template files used as **queries** by the prompt-based benchmark. The benchmark retrieves chunks and (optionally) generates answers for each template.

You can use templates in two ways:

1. **Templates in this folder** – Add or edit `.txt` files here; the benchmark loads all of them.
2. **Generated templates** – Use the generator to create more templates from a config or built-in presets (so you're not limited to what's in the folder).

---

## Using the benchmark (folder templates)

```bash
# From project root; uses prompts-template/ by default
python3 run_prompt_benchmark.py

# Or specify directory
python3 run_prompt_benchmark.py --prompts-dir prompts-template
```

To use the original `prompts/` directory instead:

```bash
python3 run_prompt_benchmark.py --prompts-dir prompts
```

---

## Generating more templates

Templates are not limited to what you put in the folder. You can generate more from:

- **Config file** – `templates_config.yaml` in this directory
- **Built-in presets** – Script has extra presets you can add

### From config (default)

Generates `.txt` files from `prompts-template/templates_config.yaml` into this directory:

```bash
python3 generate_prompt_templates.py
```

### Add built-in presets (config + extra templates)

Writes templates from the config **and** built-in presets (e.g. short_simple_math, medium_programming_security):

```bash
python3 generate_prompt_templates.py --add-builtin
```

### Built-in only (no config)

Ignore the config and write only the script’s built-in presets:

```bash
python3 generate_prompt_templates.py --builtin-only
```

### Other options

- `--config PATH` – Use a different YAML config
- `--output-dir PATH` – Write `.txt` files to another directory (e.g. a second set of prompts)
- `--no-overwrite` – Do not overwrite existing `.txt` files
- `-q` – Less output

After generating, run the benchmark as usual; it will pick up the new `.txt` files in `--prompts-dir`.

---

## Config format (`templates_config.yaml`)

Each preset has:

- **name** – Used for the filename (e.g. `short_simple_greeting` → `short_simple_greeting.txt`)
- **type** – For benchmark categorization: `simple`, `programming`, `architecture`, `non_programming`
- **length** – For categorization: `short`, `medium`, `long`, `extra_long`
- **body** – The prompt text (single line or multi-line YAML)

Example:

```yaml
presets:
  - name: short_simple_help
    type: simple
    length: short
    body: "I need help with this."

  - name: medium_non_programming_explanation
    type: non_programming
    length: medium
    body: |
      Explain the main concepts in simple terms for a non-expert audience.
      Use analogies and examples where helpful.
```

Edit `templates_config.yaml` to add your own presets, then run `python3 generate_prompt_templates.py` to regenerate the `.txt` files.

## Reference/Credit to:
https://github.com/alexziskind1/machine_tests/tree/main/ml/auto_prompter/prompts
