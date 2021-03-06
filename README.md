# sqltext
![GitHub Workflow Status](https://img.shields.io/github/workflow/status/sasakiyori/sqltext/Main)
![License](https://img.shields.io/github/license/sasakiyori/sqltext)
![GitHub release (latest SemVer)](https://img.shields.io/github/v/release/sasakiyori/sqltext)
[![Coverage](https://coveralls.io/repos/github/sasakiyori/sqltext/badge.svg?branch=main&service=github)](https://coveralls.io/github/sasakiyori/sqltext)
[![GoReportCard](https://goreportcard.com/badge/sasakiyori/sqltext)](https://goreportcard.com/report/github.com/sasakiyori/sqltext)

## Table of contents
  - [Background](#background)
  - [Features](#features)
  - [Installation](#installation)
  - [Usage](#usage)
  - [Contributing](#contributing)
  - [License](#license)

## Background
In some scenarios, programs will receive a plain sql text from upstream and then transfer to others or execute it locally.

We can't expect the sql text is always concise and highly readable, because the habits of sql writers are different. This will confuse coders when they want to do some analysis out of database tools. Since the sql text may has messy format with a lot of comments, meaningless blank spaces and line feeds, we may need some methods to simplify the sql text.

Also the logic of a sql text can be very complex, we may need a method to find out what it does and what it affects.

## Features
This repository supports simple grammar analysis and plain text simplifying for different query languages.

|                   | mysql  | postgresql         | ...     |
| :----:            | :----: | :----:             | :----:  |
| Simplify Text     |        | :heavy_check_mark: |         |
| Get Command Type  |        | :heavy_check_mark: |         |

## Installation

```shell
go get github.com/sasakiyori/sqltext
```

## Usage
```go
// use New() to create a processor with a specific sql type
processor := sqltext.New(sqltext.Postgresql)
// or use the specific sql type function to create a processor
processor = sqltext.WithPostgresql()

// only remove comments
rc := processor.RemoveComments(text)
// remove comments, then decrease blank spaces and line feeds, finally get an one-line sql text.
ft := processor.FormatText(text)

// get the command type of sql text
cmdType := processor.CommandType(text)
// maybe you only consider about if the sql text is involved in write-operation or not
readonly := processor.Readonly(text)

```

## Contributing
[Issues](https://github.com/sasakiyori/sqltext/issues/new) and [PRs](https://github.com/sasakiyori/sqltext/pulls) are welcome!

This project is just starting, lack of massy documentations, method completions, query language extensions and test case coverages. Thanks in advance to all contributors of this repository :heart:

## License
[MIT License](LICENSE)
