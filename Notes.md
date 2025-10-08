# 🧾 YAML — The Complete, Extremely Detailed Guide (Lecture Notes)

---

## 🧰 1. **Introduction: Why YAML Matters**

YAML is one of the most **important configuration languages** used in modern software engineering, DevOps, and cloud computing.

It’s widely used for:

- 🐳 **Docker**, Docker Compose & **Kubernetes**
  → For writing container orchestration configuration files.

- 🤖 Writing **CI/CD pipelines**
  → Especially in GitHub Actions (`.github/workflows/*.yml`), GitLab CI/CD, and Jenkins.

- 🖥️ **Server configurations** and Infrastructure as Code (IaC)
  → E.g., Ansible playbooks, Terraform cloud-init, Helm charts.

👉 If your work involves **automation, cloud, containers, or deployment**, YAML is not optional — it’s **vital**.

---

## 🧾 2. **What is YAML Exactly?**

- YAML stands for:

  > **YAML Ain’t Markup Language** ✅

  (This is a _recursive acronym_ — a playful way to say it’s not a markup language like HTML or XML.)

- YAML is a **human-readable data serialization language**.

  - It’s used to **represent data structures** in text files.
  - It’s especially great for **configuration files**, because it’s clean and readable.

- Other popular **data serialization formats**:

  - **XML** — verbose, markup style, angle brackets
  - **JSON** — structured, but more punctuation-heavy
  - **YAML** — minimal syntax, easier to read and edit manually.

- YAML is often considered a **superset of JSON**:

  - Any valid JSON can be expressed in YAML.
  - YAML is just more human-friendly (no curly braces, commas, or strict quotes).

✅ YAML is used to _describe_ data, not to _execute_ instructions.

---

## 🧮 3. **A Story: Why YAML Became Even More Important**

> 💬 “AI is the game of tokens.”

- **In AI systems** (e.g., ChatGPT, Claude), every character counts toward your token usage.

  - Tokens are consumed based on how much data you send.
  - Characters like `{}`, `,`, `.`, `-`, em-dashes, etc., are **counted as tokens**.

- Many developers send data in JSON to LLMs.

- Founder of Bun — **Jarred Sumner** — tweeted about experimenting with YAML:

  - Instead of sending **JSON**, he sent **YAML** in Bun docs.
  - Result:

    - **Token usage dropped by 20–25 %**
    - Better performance and lower cost
    - Faster response times

👉 **Moral**: YAML is not just a DevOps tool. It can even **optimize AI system performance**.

---

## 🧭 4. **File Setup & Tooling**

### 📁 File Naming

YAML files commonly use:

```
filename.yml
```

or

```
filename.yaml
```

Both extensions work, but `.yml` is more commonly seen in CI/CD workflows.

👉 Example:

```
chai.yml
```

---

### 🧰 Debugging YAML

- YAML is **very sensitive** to spacing, indentation, and syntax.
- Debugging errors can be a **nightmare** because:

  - Error messages are often vague.
  - They don’t tell you _exactly where_ the problem is.
  - Missing a single space can break everything.

**Recommended**: Install the **YAML Language Support by Red Hat** extension in Visual Studio Code.

Benefits:

- Real-time syntax highlighting
- Schema validation
- Error squiggles
- Auto-completion

💡 YAML support today is **much better than 3–4 years ago**.

---

## 🧩 5. **Core YAML Concept: Key–Value Pairs**

YAML uses a **key: value** structure.

```yaml
chai_type: masala_chai
```

- **Key** → `chai_type`
- **Value** → `masala_chai`

### ✅ Best Practices

- Use **underscores** in keys:

  ```
  chai_type
  ```

- You can also use **dashes**, but underscores are more common:

  ```
  chai-type
  ```

- Keys should be simple and descriptive.

---

## 🧭 6. **Version Specification**

- Often, the first line in a YAML file is:

```yaml
version: 3.2
```

⚠️ Important:

- This is **not** the YAML language version.
- This refers to the **version of the tool or API** the configuration is written for.

  - Example: Docker Compose version, Kubernetes API version, CI/CD pipeline version.

---

## 📝 7. **Comments in YAML**

```yaml
# This is a single-line comment
```

- Use `#` for comments.
- For multiple lines:

```yaml
# Line 1
# Line 2
# Line 3
```

- There’s no special multi-line comment syntax in YAML (unlike some programming languages).

✅ Use comments generously to explain configurations — especially in complex DevOps files.

---

## 📐 8. **Indentation Rules**

- YAML is **whitespace sensitive**.
- **Use spaces** — ❌ no tabs.
- Standard indentation: **2 spaces** per level.

Example:

```yaml
chai_recipe:
  base: black_tea
  milk: whole_milk
```

⚠️ A single misplaced space can cause parsing errors.
This is why linters and extensions are strongly recommended.

---

## 🧠 9. **Data Types in YAML**

YAML supports multiple data types:

- Strings
- Numbers
- Booleans
- Null
- Timestamps
- Collections (Lists and Maps)
- Sets
- Custom types

---

### 🧾 9.1 Strings

```yaml
chai_name: Masala Chai
description: "Chai with cardamom, ginger"
tagline: "The best chai in town"
```

- **No quotes**: when value is simple (letters, numbers, underscores).
- **Double quotes `"`**: when value contains special characters (`&`, `$`, etc.).
- **Single quotes `'`**: when value contains text that should not be interpreted in any way.

#### 🔸 Special Character Handling

```yaml
chai_name: "Masala & Chai"
```

Using double quotes avoids misinterpretation of `&`.

---

### 📜 9.2 Multi-line Strings — Block Scalar `|`

```yaml
brewing_instructions: |
  boil water
  add tea leaves
  add milk
```

- `|` preserves line breaks.
- This is useful for:

  - Writing long text
  - Descriptions
  - Scripts

If indentation is missing after `|`, you’ll get errors like:

```
implicit keys need to be on a single line
implicit map keys need to be followed by map values
```

✔ Correct:

```yaml
brewing_instructions: |
  boil water
  add tea leaves
  add milk
```

❌ Incorrect:

```yaml
brewing_instructions: |
boil water
add tea leaves
add milk
```

---

### 📜 9.3 Folded Multi-line Strings — `>`

```yaml
brewing_instructions: >
  boil water
  add tea leaves
  add milk
```

- `>` folds newlines into spaces.
- Useful for **long text blocks that should be rendered as one line**.

---

## 🔢 9.4 Numbers

```yaml
cups_per_day: 3 # Integer
cups_per_day_two: 3.5 # Floating-point
cups_per_day_three: 3.5e+2 # Exponential notation
hexadecimal: 0xFF22FF # Hexadecimal
octal_number: 08 # Octal
```

YAML auto-detects numeric formats.

---

## 🔘 9.5 Booleans

```yaml
is_hot: true
add_sugar: yes
add_salt: no
instant: off
```

- YAML supports multiple boolean syntaxes:

  - `true` / `false` ✅ (recommended)
  - `yes` / `no`
  - `on` / `off`

---

## 🕳️ 9.6 Null Values

```yaml
sweetner: null
alternative_milk: ~
```

- `null` and `~` both denote a null value.
- Commonly used to **disable optional config**.

---

## 🕒 9.7 Timestamps

```yaml
morning_brew: 2025-01-15
local_time: 2025-01-15 08:30:01
```

- YAML automatically parses ISO-formatted timestamps.
- Time zone handling may depend on the parser.

---

## 🧂 10. **Collections (Lists and Maps)**

### 📜 10.1 Lists (Sequences)

```yaml
spices:
  - ginger
  - cloves
  - black_pepper
  - true
  - 200
```

- `-` starts a new list item.
- List values can be strings, numbers, booleans, or nested objects.

Alternative inline format:

```yaml
spices: [cardamom, ginger, cloves]
```

---

### 📊 10.2 Nested Lists (Lists of Maps)

```yaml
chai_categories:
  - name: Traditional
    varieties:
      - Masala Chai
      - Ginger Chai
      - Cardmom Chai
  - name: Modern
    varieties:
      - Vanilla Chai
      - Chocolate Chai
```

- Very common in configuration files (e.g., multiple services, jobs, or containers).
- Indentation is **critical** here.

---

## 🧭 11. **Dictionaries / Maps**

### 📘 Simple Dictionary

```yaml
masala_chai:
  ingredients:
    tea: black_tea
    liquid:
      water: 200ml
      milk: 100ml
    spices:
      ginger: 1_inch
      cinnamon: 1_stick
  preparation:
    method: simmer
    duration: 5_minutes
```

- Key–value hierarchy is shown through indentation.
- Each level can contain either:

  - Another dictionary (map)
  - A list
  - A scalar (string, number, etc.)

---

## 🧾 12. **List of Dictionaries**

Commonly used in Docker, GitHub Actions, Kubernetes, etc.

```yaml
chai_menu:
  - name: Masala_Chai
    price: 30
    size: regular
  - name: Ginger_Chai
    price: 30
    size: regular
```

✅ Great for representing **multiple similar entities** (e.g., services, jobs, steps).

---

## 🧭 13. **Anchors & Aliases (Reusability)**

YAML allows **referencing** blocks to avoid repetition.

- `&` → Anchor (defines reusable block)
- `*` → Alias (refers to anchor)
- `<<` → Merge key (inject anchor content)

```yaml
default_chai_base: &default_base
  tea: black_tea
  water: 200ml
  brewing_time: 5

morning_chai:
  <<: *default_base
  milk: 100ml

evening_chai:
  <<: *default_base
  milk: 200ml
```

✔ Benefits:

- DRY (Don’t Repeat Yourself)
- Consistency across multiple configs
- Easier maintenance

---

## 🏷️ 14. **Explicit Data Typing**

Sometimes you want to force YAML to treat a value as a **specific type**.

```yaml
zip_code: !!str 12345 # Force as string, not number
count: !!int "123" # Force as integer
```

✅ Useful when:

- Leading zeros must be preserved (e.g., zip codes)
- Numeric values must remain as strings.

---

## 🧂 15. **Sets in YAML**

YAML supports `!!set` to define **unique collections**.

```yaml
unique_spices: !!set
  ? cardamom
  ? ginger
  ? cloves
```

- Each element is a **key** in a set.
- No duplicates are allowed.

---

## 🧱 16. **Custom Types**

- YAML allows creating **custom data types**.
- These are typically used with **schemas or custom parsers**.
- Example:

  ```yaml
  custom_tag: !mytag
    some_data: 123
  ```

- Useful in domain-specific tools or custom parsers.

---

## ⚠️ 17. **Common YAML Pitfalls (and Fixes)**

| Mistake                    | Problem                                  | Fix                         |
| -------------------------- | ---------------------------------------- | --------------------------- |
| ❌ Tabs                    | YAML doesn’t allow tabs                  | Use spaces only             |
| ❌ Missing space after `-` | Parse error                              | Add space after `-`         |
| ❌ Misaligned indentation  | “Unexpected key” or “implicit key” error | Keep indentation consistent |
| ❌ Special chars unquoted  | Parse error                              | Wrap in double quotes       |
| ❌ No proper nesting       | Breaks structure                         | Verify spacing with linter  |

👉 Always lint and format YAML automatically using editor extensions or CI tools.

---

## 🧭 18. **Where YAML is Used in Real Projects**

1. 🐳 **Docker / Docker Compose**

   - `docker-compose.yml` → defines services, networks, volumes.

2. ☸ **Kubernetes Manifests**

   - `deployment.yaml`, `service.yaml`

3. 🤖 **GitHub Actions Workflows**

   - `.github/workflows/ci.yml`

4. ⚡ **CI/CD Pipelines**

   - e.g., GitLab CI, Jenkins pipelines.

5. 🧱 **Infrastructure as Code (IaC)**

   - Ansible playbooks, Helm charts.

6. 🧠 **AI / LLM Context Data**

   - YAML used to reduce token cost in prompt structures.

📎 [GitHub Actions Documentation](https://docs.github.com/en/actions)

---

## 🧭 19. **YAML vs JSON**

| Feature              | YAML                     | JSON                   |              |
| -------------------- | ------------------------ | ---------------------- | ------------ |
| Readability          | Human-friendly, clean    | More punctuation-heavy |              |
| Comments             | ✅ Supported (`#`)       | ❌ Not supported       |              |
| Indentation          | Meaningful (spaces only) | Not meaningful         |              |
| Braces & punctuation | Minimal                  | Required               |              |
| Multiline strings    | ✅ Easy with `           | `and`>`                | ❌ Difficult |
| Token usage in LLMs  | Lower                    | Higher                 |              |
| File size            | Smaller                  | Larger                 |              |
| Human editing        | Easy                     | Cumbersome             |              |

---

## 🧪 20. **Final Example: `chai.yml`**

Below is a complete YAML file combining most concepts we learned:

```yaml
# --------------------------------------------------
# YAML Example: chai.yml
# Demonstrating multiple YAML features together
# --------------------------------------------------

version: 3.2 # Tool configuration version (e.g., Docker or CI/CD)

# Basic key-value pair
chai_type: masala_chai

# Nested map (dictionary)
chai_recipe:
  base: black_tea
  milk: whole_milk

# Block scalar (preserves newlines)
brewing_instructions: |
  boil water
  add tea leaves
  add milk

# Simple list (modern)
spices:
  - ginger
  - cloves
  - black_pepper

# List of dictionaries
chai_menu:
  - name: Masala_Chai
    price: 30
    size: regular
  - name: Ginger_Chai
    price: 30
    size: regular

# Anchors & Aliases for DRY configs
default_chai_base: &default_base
  tea: black_tea
  water: 200ml
  brewing_time: 5

morning_chai:
  <<: *default_base
  milk: 100ml

evening_chai:
  <<: *default_base
  milk: 200ml

# Explicit typing
zip_code: !!str 12345

# Set (unique values)
unique_spices: !!set
  ? cardamom
  ? ginger
  ? cloves
```

---

## 📎 21. **Useful Links & References**

- 📄 [GitHub Actions Documentation](https://docs.github.com/en/actions) — real YAML CI/CD examples
- 🐳 [Docker Compose Reference](https://docs.docker.com/compose/)
- ☸ [Kubernetes YAML Manifests](https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/)
- 🧰 [YAML Specification](https://yaml.org/spec/)
- 🧩 [YAML Language Support (VS Code)](https://marketplace.visualstudio.com/items?itemName=redhat.vscode-yaml)

---

## 🧭 22. **Pro Tips from the Lecture**

- Always install the **Red Hat YAML extension** for VS Code.
- Always use **spaces**, not tabs.
- Use **anchors** for repeated data.
- Use **block scalars** for multiline strings.
- Explicitly type data when needed (e.g., `!!str` for zip codes).
- Check indentation if you get vague errors like:

  - `implicit keys need to be on a single line`
  - `implicit map keys need to be followed by map values`

<!-- YAML

- used in learning docker, docker compose & kubernates
- writing github's cicd pipelines
- to do server configurations

If you want to do anything like that, then YAML is vital for your work.

YAML

- it is a data serialization format

Other data serialization formats are:

- XML
- JSON

Few people say that YAML is superset of JSON

A story which tells why YAML is important:

- AI is the game of tokens. Token is consumed on the basis of how much content is given. For more data, curly braces, dot, comma, hyphen, mdashes, all are counted .

You may have seen in docs some like "read with chatgpt", "read with anthropic".There is a founder of bun named "Jarred Sumner". He tweeted where other documentations are sending their data in json format to chatgpt and other, he started trying to send data in yaml in the bun docs. Now what it does?
It upgraded the performance of tokens upto 20-25 % because those curly braces and other were left.

Intresting?
That is why we should learn yaml.

The full form of YAML is:

YAML Ain't Markup Language ✅

It’s a recursive acronym, meaning its name is a playful way of saying it’s not a markup language like XML or HTML, but rather a human-readable data serialization language used for configuration files, data exchange, and more.

make file "chai.yml":

Before starting yaml, we need extensions.
Debugging in yaml is nightmare because we dont know where is problem as there is not very good error responses in yaml

install YAML extension of red hat.

By default the support for yaml is also very improved compared to 3-4 years before.

We write configuration in yaml so most of the time we play with key- value pairs.
Underscore is mostly preferred in yaml but you can use dashes if you dont want to use it.

How key-value pairs?

chai_type: masala_chai

Most of the time, you will see that in the first line mostly version is written.

version: 3.2

This is not the version of the yaml
This is verion for which we are writing configurations like for docker, kubernated, cicd piperlines.

# inline comment in yaml

You have to use this # multiple times for multi-line comments.

The thing to remember in yaml is indentations.
You always use spaces not tabs.
Usually, you give two spaces for indentation.

chai_recipe:
base: black_tea
milk: whole_milk

chai_receipe_two:
base: black_tea
milk: whole_milk

Datatypes:

String
chai_name: Masala Chai
description: "Chai with cardamon, ginger"
tagline:'The best chai in town'

We will learn where it is better to use quotes.

brewing_instructions: |
boil water
add tea leaves
add milk

You will see an error here, "implicit keys needs to be on a single line ", "implicit map keys need to be followed by map values"
That is why finding error in yaml is nightmare

Note that indentation is missing, (2 spaces)

Like this

```
brewing_instructions: |
  boil water
  add tea leaves
  add milk
```

Sometime we will also see something like this,
both are multi-folded comments

brewing_instructions: >
boil water
add tea leaves
add milk

Note: Whenever we want to write any special symbols like $, & , we should use double quotes as these special symbols have their own meaning
Eg: chai_name: "Masala & Chai"

Numbers:

cups_per_day: 3
cups_per_day_two: 3.5
cups_per_day_two: 3.5e + 2
hexadecimal: 0xFF22FF
We can also write octals using 08.

Booleans:

is_hot: true
add_sugar: yes
add_salt: no
instant: off

We usually try to use true/false.
But other are also supported.

Null Values:

sweetner: null
alternative_milk: ~

~ denotes null

Timestamps

morning_brew: 2025-01-15
local_time: 2025-01-15 08:30:01

Collections

```
spices:
  - ginger
  - cloves
  - black_pepper
  - true
  - 200
```

This is used todays

spices: [cardamom, ginger, cloves]
This is old format.

steeping_times: [3, 2, 1]

We also have nested lists

```
chai_categories:
  - name: Traditional
    varieties:
      - Masala Chai
      - Ginger Chai
      - Cardmom Chai
  - name: Modern
    varieties:
      - Vanilla Chai
      - Chocolate Chai
```

This becomes very complex to comprehend and prone to error:

```
masala_chai:
  ingredients:
    tea: black_tea
    liquid:
      water: 200ml
      milk: 100ml
    spices:
      ginger: 1_inch
      cinnamon: 1_stick
  preparation:
    method: simmer
    duration: 5_minutes

```

List of Dictionaries & Dictionaries of List

```
chai_menu:
  - name: Masala_chai
    price: 30
    size: regular

  - name: Ginger_Chai
    price: 30
    size: regular
```

Advanced Feature
&default_base is anchors or aliases
<< to refer to anchor

```
default_chai_base: &default_base
  tea: black_tea
  water: 200ml
  brewing_time: 5

morning_chai:
  <<: *default_base
  milk: 100ml

evening_chai:
  <<: *default_base
  milk: 200ml


```

Multiline keys also exists

Explicit data typing
What if we want this zip_code to be treated string.

zip_code: !!str 12345
count: !!int "123"

We can also make sets

```
unique_spices: !!set
  ? cardamom
  ? ginger
  ? cloves
```

We can also make custom types in yaml

Indentation is main problem in yaml

You can see examples of yaml in github actions page -->
