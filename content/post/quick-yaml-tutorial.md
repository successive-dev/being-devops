---
title: "Quick Yaml Tutorial"
date: 2023-05-27T21:59:52+05:30
publishdate: 2023-05-27
lastmod: 2023-05-27
draft: false
tags: ["yaml", "tutorial", "quick"]
---

YAML is a human-readable data serialization language. It stands for "YAML Ain't Markup Language". YAML files use a simple syntax to represent data structures like lists, dictionaries, and key-value pairs. Here are some basic concepts:

1. YAML syntax uses indentation to define nesting. Use two spaces for each level of indentation.
2. Comments start with the "#" character.
3. Lists are represented by dashes ("-").
4. Key-value pairs are represented by a colon (":").

Here's an example YAML document:

```yaml
# This is a YAML file
name: John Smith
age: 30
address:
  street: 123 Main St
  city: Anytown
  state: NY
  zip: 12345
favorite_colors:
  - red
  - green
  - blue
```

In this example, we have a dictionary with several key-value pairs. The `address` key has a nested dictionary, and the `favorite_colors` key has a nested list.

You can also use YAML to define more complex data structures like objects, arrays, and mappings. Here's an example of a more complex document:

```yaml
# This is a YAML file
invoice:
  id: INV-001
  date: '2022-05-03'
  customer:
    name: John Smith
    email: john@example.com
    phone: '555-123-4567'
  items:
    - id: 001
      name: Item 1
      description: Some item description
      price: 10.99
      quantity: 2
    - id: 002
      name: Item 2
      description: Another item description
      price: 20.99
      quantity: 1
  subtotal: 42.97
  tax: 3.24
  total: 46.21
```

In this example, we have a nested dictionary that represents an invoice. The `customer` key has a nested dictionary, and the `items` key has a nested list of dictionaries.

YAML is widely used in configuration files for software applications, as well as for data exchange between systems. Its simple syntax and human readability make it a popular choice for these use cases.