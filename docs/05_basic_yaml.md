YAML, or "YAML Ain't Markup Language," is a human-readable data serialization format widely used for configuration files and data exchange across different programming languages. Its intuitive syntax emphasizes readability and simplicity, making it popular for various applications.

### Scalars: Strings, Numbers, and Booleans

YAML can represent basic data types straightforwardly:

- **String Example:**
  ```yaml
  string_example: Hello, YAML!
  ```

- **Number Example:**
  ```yaml
  number_example: 42
  ```

- **Boolean Example:**
  ```yaml
  boolean_example: true
  ```

### Lists

Lists in YAML allow for sequential collections of items:

- **Fruits Example:**
  ```yaml
  fruits:
    - Apple
    - Orange
    - Banana
  ```

### Mapping: Key-Value Pairs

YAML employs key-value pairs to define mappings:

- **Person Example:**
  ```yaml
  person:
    name: John Doe
    age: 30
    city: New York
  ```

### Nested Structures: List of Dictionaries

YAML supports nesting, enabling complex data structures:

- **Family Example:**
  ```yaml
  family:
    parents:
      - name: Jane
        age: 50
      - name: John
        age: 52
    children:
      - name: Jimmy
        age: 22
      - name: Jenny
        age: 20
  ```
