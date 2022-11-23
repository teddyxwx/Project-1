# Project 1: JSON

<sup><sub>This project is based on [jsoncpp](https://github.com/open-source-parsers/jsoncpp) [1.9.5](https://github.com/open-source-parsers/jsoncpp/releases/tag/1.9.5) licensed under [MIT](https://spdx.org/licenses/MIT.html).</sub></sup>

## Introduction

> You can skip this section if you are familiar with JSON.

[JSON](https://www.json.org/) is probably the most popular data-interchange format in the world.
To see why it is needed, lets imagine a scenario.

You are developing an instant message app, OurChat, which can send and receive messages.
Alice sends a message "Hello World!" to Bob.
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

## Tasks (max 100pts)

- [ ] Maintenance (40%pts off if not done): Setup [Codecov](https://about.codecov.io/) for your repository to track the code coverage.
    - Check below for instructions.
- [ ] C++ API (5pts): Define JSON directly in C++ with [User-defined literals](https://en.cppreference.com/w/cpp/language/user_literal).
- [ ] C++ API (5pts): Support [user-defined conversion](https://en.cppreference.com/w/cpp/language/cast_operator) to primitive types.
- [ ] Utility (5pts): Convert from and to [CSV Files](https://datatracker.ietf.org/doc/html/rfc4180).
    - An implementation as simple as comma-separated values suffices.
- [ ] Feature (10pts): Allow zero or one [trailing commas](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Trailing_commas) in JSON arrays and objects.
- [ ] Feature (10pts): Add a new type `binary` to represent binary data.
- [ ] Feature (10pts): Support string concatenation.
    - Example: `{"name": "San"+"Zhang"}` should be equivalent to `{"name": "SanZhang"}`.
    - Concatenation in keys in objects is not required.
- [ ] Feature (10pts): Add a new type `date` to represent date and time.
- [ ] Feature (10pts): Support pointers to share JSON values.
- [ ] Utility (20pts): [Schema](https://json-schema.org/learn/) validation.
    - Only need to support the keys used in the [examples collection](https://json-schema.org/learn/).
    - URL-related keywords are not required, such as `$ref`.
- [ ] Utility (10pts + 10pts): Support [XPath](https://developer.mozilla.org/en-US/docs/Web/XPath)-like query to JSON.
    - Required path selector: `.` (current node), `..` (parent node), `*` (all children), `name` (child with name `name`), array index (e.g. `[0]`).
    - Overload `operator / ()` to support path selector. No need to parse the query string.
    - Extra 10pts if you can support assignment via the query.
- [ ] Utility (20pts): Support bundling and unbundling all the contents of a folder into a JSON file.
    - You might want to combine this task with the `binary` type.
    - Metadata of the files do not need to be preserved.
    - You might want to enable C++ 17 to use `std::filesystem` by `set(CMAKE_CXX_STANDARD 17)` in `CMakeLists.txt`.
- [ ] Performance (50pts): JSON minifier using pointers.
    - Minify the output size of JSON by removing unnecessary characters.
    - You probably want to combine this task with the task of pointer support and string concatenation.
- [ ] Utility (50pts): Make a terminal UI for easy browsing & editing JSON.
    - A tree view (or better) interface is required. Use [ncurses](https://invisible-island.net/ncurses/announce.html), [FTXUI](https://github.com/ArthurSonzogni/FTXUI), or something else to prettify the output.
    - A screenshot of the terminal UI should be included in README.
    - The libraries should be embedded inside the repository. Don't forget to include the license files!
- [ ] Performance (50pts): Add indexing support for JSON to support random read on disk without loading the full file in memory.
    - The index should be stored in the same file.
    - The JSON file should still be able to be parsed correctly with your program.
- [ ] Other (50pts): Anything else you can think of.
    - The score is judged by usefulness, difficulty, and implementation quality.

As seen from the first task,
tests consist of 40% of the total score in this project.
Each implemented feature should contain **reasonable** tests in order to get full points.
The specific test requirements for each task are **not** revealed
since it is part of the project to design the API and the tests.

## Report

After you finish a task,
you should tick the checkbox here in `README.md`,
and briefly summarize what you did in the list above.

A clear and well-organized summary helps TAs to understand your work better.
If you don't think a detail is worth mentioning,
neither does the reader.
Sometimes a screenshot is worth a thousand words.

A bad example:

> - [x] Feature (10pts): Add a new type `date` to represent date and time.
>     - A C++ class `Date` is added to represent date information.
>     - Added a new switch branch in `json_reader` to parse date strings.
>     - Added a serialization function to `json_writer` to convert `Date` to string.
>     - Test: Input data with "data" field can be parsed correctly.
>     - Test: Converting JSON with "date" field to string outputs expected results.
>     - Test: Invalid date strings are rejected.
>     - Other tests are still passed after the changing the code.

A (too) good example:

> - [x] Feature (10pts): Add a new type `date` to represent date and time.
>     - Support date in ISO 8601 format.
>     - Distinguish date from string with quotes "`"`".
>     - Distinguish date from numbers using `isNumber()`.
>     - Test: Valid date strings are not parsed as numbers or strings.
>     - Test: Use substrings of valid date strings to generate erroneous date strings.

## Guides

### Getting Started

As always, you need a working C++ compiler and CMake installed on your system.

You might find the following files helpful:

* `include/json/value.h`.
* `src/lib_json/json_reader.cpp`.

A few examples of the API are given in [`example/`](example/).

For the usage of existing source code, see the original [Wiki](https://github.com/open-source-parsers/jsoncpp/wiki)
and [API document](http://open-source-parsers.github.io/jsoncpp-docs/doxygen/index.html).

### Adding a new executable

If you write a new program with `main()` function,
you need to add a new executable to `CMakeLists.txt`:

```cmake
add_executable(my_executable path/to/my_executable.cpp)
target_link_libraries(my_executable jsoncpp_static)
```

in order to compile and link it with the JSON library.

### Setting-up Codecov

Codecov requires admin access from the organization so TA will open up access for you
**after you have accepted the homework in github classroom**.
This might take 2-3 days depending on the workload of the TA.

After the setup is done,
TODO

### Testing

To do testing, Python3 is required.

Run test from "Testing"(测试) section on the top of Visual Studio,
or in the terminal:

```bash
cd build/ # Go to your build directory
ctest
```

## Adding a reader/writer test

Tests are stored in `test/data`.
To add a test, you need to create two files:

* a `TESTNAME.json` file, that contains the input document in JSON format.
* a `TESTNAME.expected` file, that contains a flatened representation of the
  input document.

The `TESTNAME.expected` file format is as follows:

* Each line represents a JSON element of the element tree represented by the
  input document.
* Each line has two parts: the path to access the element separated from the
  element value by `=`. Array and object values are always empty (i.e.
  represented by either `[]` or `{}`).
* Element path `.` represents the root element, and is used to separate object
  members. `[N]` is used to specify the value of an array element at index `N`.

See the examples `test_complex_01.json` and `test_complex_01.expected` to better understand element paths.

When a test is run, output files are generated beside the input test files. Below is a short description of the content of each file:

* `test_complex_01.json`: input JSON document.
* `test_complex_01.expected`: flattened JSON element tree used to check if
  parsing was corrected.
* `test_complex_01.actual`: flattened JSON element tree produced by `jsontest`
  from reading `test_complex_01.json`.
* `test_complex_01.rewrite`: JSON document written by `jsontest` using the
  `Json::Value` parsed from `test_complex_01.json` and serialized using
  `Json::StyledWritter`.
* `test_complex_01.actual-rewrite`: flattened JSON element tree produced by
  `jsontest` from reading `test_complex_01.rewrite`.
* `test_complex_01.process-output`: `jsontest` output, typically useful for
  understanding parsing errors.

## Adding a test for custom data types

Under `src/jsontestrunner/main.cpp`,
the `printValueTree()` function is used to serialize the values in JSON,
in order to compare line-by-line in the `.expected` files.
