
# ⚠️⚠️ Warning: Work in Progress ⚠️⚠️

**This project is currently under development** and is **not yet stable**. Only the `get` method has been tested. Please use with caution, and feel free to report issues or contribute to its development.

---

# @robusto/fetch

`@robusto/fetch` is a ReScript library that wraps the native `fetch` API to provide a more developer-friendly experience. It simplifies HTTP requests (GET, POST, PUT, DELETE) with better type safety and cleaner APIs. This library is designed to enhance developer productivity with intuitive request handling and result parsing.

## Features

- Simplified `fetch` requests for ReScript developers
- Type-safe handling of request results
- Automatic JSON parsing and error handling
- Currently, only `get` has been tested

## Installation

You can install the library from npm using the following command:

```sh
npm install @robusto/fetch
```

## Usage

After installing, you can use `@robusto/fetch` in your ReScript project.

1. Add `@robusto/fetch` to your `bsconfig.json`:

```json
{
  "name": "your-project",
  "sources": [
    {
      "dir": "src",
      "subdirs": true
    }
  ],
  "bs-dependencies": ["@robusto/fetch"]
}
```

2. Example usage of `get` with a parser:

```rescript
open FetchRobusto

let parserString = (response: string): result<string, string> => {
  Ok(Js.Json.deserializeUnsafe(response))
}

let res = await useFetch("https://jsonplaceholder.typicode.com", Dict.make())["get"](
  "/todos/1",
  parserString,
)

switch res {
| Ok(data) => Js.log("Data:", data)
| Error(err) => Js.log("Error:", err)
}
```

### API

### `useFetch(domainUrl: string, headers: Js.Dict.t<string>)`

Returns an object with the following methods:

- `get(path: string, parser: string => result<'response, string>): Promise<Result<'response, string>>`
- `post(path: string, body: 'a): Promise<Result<string, string>>`
- `put(path: string, body: 'a): Promise<Result<string, string>>`
- `delete(path: string): Promise<Result<string, string>>`

### Methods Overview

- **get**: Makes a `GET` request to the specified path. It accepts a parser to process the response.
- **post**: Sends a `POST` request with a body. The body is automatically stringified if it's not a string.
- **put**: Similar to `post`, but uses the `PUT` method.
- **delete**: Makes a `DELETE` request.

## Development Commands

- Compile the project: `npm run res:build`
- Clean the build artifacts: `npm run res:clean`
- Watch for file changes and recompile: `npm run res:dev`

## Status

This library is currently in development, and only the `get` method has been tested. Use it at your own risk, and expect breaking changes as the project evolves.
