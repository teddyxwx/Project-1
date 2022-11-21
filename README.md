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

As always, you need a working C++ compiler and CMake installed on your system.
Additionally, Python3 is required to run the tests.

You might find the following files helpful:

* `include/json/value.h`.
* `src/lib_json/json_reader.cpp`.

For the usage of existing source code, see the original [Wiki](https://github.com/open-source-parsers/jsoncpp/wiki)
and [API document](http://open-source-parsers.github.io/jsoncpp-docs/doxygen/index.html).

To add a new executable, you need to modify `CMakeLists.txt` and `src/CMakeLists.txt`.
(TODO)

## Tasks (max 100pts)

- [ ] Maintenance (?pts): Setup [Coveralls](https://coveralls.io/) for your repository to track the code coverage.
- [ ] C++ API (?pts): Define JSON directly in C++ with [User-defined literals](https://en.cppreference.com/w/cpp/language/user_literal).
- [ ] C++ API (?pts): Allow assignment to member of an object using `[]`.
- [ ] Utility (?pts): Convert from and to CSV.
- [ ] Grammar (?pts): Allow zero or one trailing comma in JSON array and object.
- [ ] Feature (?pts): Add a new type `binary` to represent binary data.
- [ ] Feature (?pts): Add a new type `date` to represent date and time.
- [ ] Feature (?pts): Add a pointer to share JSON values.
- [ ] Feature (?pts): Support string concatenation.
- [ ] Utility (?pts): Add XPath-like query to JSON.
- [ ] Utility (?pts): [Schema](https://json-schema.org/learn/) validation.
- [ ] Utility (?pts): Zip a folder into a JSON file.
- [ ] Performance (?pts): Add indexing support for JSON to support random read.
- [ ] Performance (?pts): JSON minifier using pointers.
- [ ] Utility (?pts): Make a terminal UI for easy browsing & editing JSON.
    - Using [ncurses](https://invisible-island.net/ncurses/announce.html), [FTXUI](https://github.com/ArthurSonzogni/FTXUI), or something else to prettify the output.
    - A screenshot of the terminal UI should be included in README.
   - The libraries should be embedded inside the repository. Don't forget to include the LICENSE!
- [ ] Other (?pts): Anything else you can think of. The score is judged by usefulness, difficulty, and implementation quality.

Each implemented feature should contain **reasonable** tests in order to get full points.
Tasks without tasks get at most 50% of the points.
The specific test requirements for each task are **not** revealed
since it is part of the project to design the API and the tests.

## Report

After you finish a task,
you should tick the checkbox here in `README.md`,
and add more design details to the list above.

Remember, a clear and well-organized summary helps people to understand your work better.
If you don't think a detail is worth mentioning,
neither does the reader.
Sometimes a screenshot would help to demonstrate your work.

A bad example:

> - [ ] Feature (?pts): Add a new type `binary` to represent binary data.
> - [x] Feature (?pts): Add a new type `date` to represent date and time.
>     - A C++ class `Date` is added to represent date information.
>     - Added a new switch branch in `json_reader` to parse date strings.
>     - Added a serialization function to `json_writer` to convert `Date` to string.
>     - Test: Input data with "data" field can be parsed correctly.
>     - Test: Converting JSON with "date" field to string outputs expected results.
>     - Test: Invalid date strings are rejected.
>     - Other tests are still passed after the changing the code.
> - [ ] Feature (?pts): Add a pointer to share JSON values.

A (too) good example:

> - [ ] Feature (?pts): Add a new type `binary` to represent binary data.
> - [x] Feature (?pts): Add a new type `date` to represent date and time.
>     - Support date in ISO 8601 format.
>     - Distinguish date from string with quotes "`"`".
>     - Distinguish date from numbers using `isNumber()`.
>     - Test: Valid date strings are not parsed as numbers or strings.
>     - Test: Use substrings of valid date strings to generate erroneous date strings.
> - [ ] Feature (?pts): Add a pointer to share JSON values.
