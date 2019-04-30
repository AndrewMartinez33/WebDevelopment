# Why JSON ?

It is a very common data format used for asynchronous browser-server communication, including as a replacement for XML in some AJAX-style systems.

JSON grew out of a need for stateful, real-time server-to-browser communication protocol withouth using browser plugins such as Flash or Java applets, the dominant mehtods used in the early 2000's.

JSON is based on a basic data structure.

# What is JSON?

JSON is a textual, language-independent data-exchange format, much like XML, CSV or YAML.

- Extended from JavaScript
- Media type is application/jason
- File extension is .json
- Always starts and ends with { }
- name and values are separated by a colon :
- name-value pairs are separated by a comma ,

```json
// key/name value pairs separated by colon
{ "name": "value"}

// pairs are separated by a comma
{ "name": "value", "name2": "value", "name3": "value"}

// arrays have square brackets separated by a comma
{ "name": [ {"name": "value", "name2": "value", "name3": "value"} ] }

```

# Data Types in JSON

- Number - double - precision floating-point can be digits, positive or negative, decimal fractions, exponents, etc.
- String - Must be double quoted, Unicode with backslash escaping
- Boolean - true or false
- Array - [ ordered ]
- Object - { unordered }
- Null - empty

# Example

```json
let person = {
  "Name": "Joe",
  "Last Name": "Miller",
  "Address": {
    "Street": "Neverland 42",
    "City": "Toronto"
  },
  "Hobbies": [
    "doing stuff",
    "dreaming"
  ],
  "Cars": [{
    "make": "Mustang",
    "year": 2018,
    "color": "red"
    },
    {
    "make": "F150",
    "year": 2015,
    "color": "blue"
    }
  ]
}

```
