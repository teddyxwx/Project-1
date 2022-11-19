# Project 1: JSON

<sup><sub>This project is based on [jsoncpp](https://github.com/open-source-parsers/jsoncpp) [1.9.5](https://github.com/open-source-parsers/jsoncpp/releases/tag/1.9.5) licensed under [MIT](https://spdx.org/licenses/MIT.html).</sub></sup>

- [ ] https://coveralls.io/

## Introduction

> You can skip this section if you are familiar with JSON.

[JSON](https://www.json.org/) is probably the most popular data-interchange format in the world.
To see why it is needed, lets imagine a scenario.

You are developing an instant message app, OurChat, which can send and receive messages.
Alice send a message "Hello World!" to Bob.
The message sent by the program would look like:

```
Hello World!
```

Now Bob wants to know when the message was sent.
Alice can add a timestamp to the message:

```
Hello World! (sent at 2019-01-01 12:00:00)
```

A new user, Charlie, starts using OurChat.
If Charlie also sends a message to Bob,
Bob want to know who sent the message.
You would need to add the sender's name to the message:

```
Hello World! (sent at 2019-01-01 12:00:00) - Charlie
```

The message is getting longer and longer.
The more information is added to the message,
the harder it is to read.
The receiver of the message would need to parse the message
to get the information without ambiguity.
This is where JSON comes in.

JSON is a simple formal language for representing structured data.
It defines six types of values:

- `null`: `null` represents the absence of a value.
- `boolean`: Either `true` or `false`.
- `number`: A signed decimal number. Examples: `2022`, `-1.5`, `1e9`.
- `string`: A sequence of characters. Examples: `"Hello World!"`.
- `array`: An ordered sequence of values (of any type). Examples: `[1, 2, "Hello", null]`.
- `object`: An unordered collection of key-value pairs.
  The keys have to be strings, but the values can be any type.
  Examples: `{"name": "Alice", "age": 20}`.

You might have noticed that JSON is not type-safe:
any value can appear in any place.
This is a natural consequence of the fact that JSON is a data-interchange format.
It is suitable for dynamic languages like JavaScript and python,
though it's a little bit tricky to use in static languages like C++.
In this project, we work on a C++ library for JSON
to explore how to design a type-safe dynamic library in C++.

## Getting Started

[JsonCpp-documentation]: http://open-source-parsers.github.io/jsoncpp-docs/doxygen/index.html

If you have trouble, see the [Wiki](https://github.com/open-source-parsers/jsoncpp/wiki), or post a question as an Issue.
