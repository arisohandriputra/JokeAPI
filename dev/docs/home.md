# JokeAPI - Developer Documentation [WIP]
This documentation is up to date with version [`2.4.0`](../../changelog.md#240)  
It is under heavy construction, please don't expect much.  
  
This is a documentation on the internals of JokeAPI.  
Use it to get to know how the API works and to learn about its quirks.  
  
Note that it can be incomplete or inaccurate due to how many times I change the API.  
So I recommend the practice of learning by doing, additionally to what you find here.  
  
Please read through this file first.  
Afterwards, refer to the following topics to learn about every aspect of the API:  

<br>

### Table of Contents:
- **Home**
    - [Important Information](#important-information)
    - [Knowledge Prerequisites](#knowledge-prerequisites)
    - [Technical Prerequisites](#technical-prerequisites)
    - [Miscellaneous Concepts](#miscellaneous-concepts)
        - [Category Aliases](#category-aliases)
        - [Filter Components](#filter-components)
- **Other Topics**
    - [How to set up JokeAPI](./setup.md#readme)
    - [Code Style](./code-style.md#readme)
    - [WIP - Execution Flow](./execution-flow.md#readme)
    - [Docs Compilation](./docs-compilation.md#readme)
    - [Endpoints](./endpoints.md#readme)
    - [File Format Conversion](./file-format-conversion.md#readme)
    - [WIP - Translations](./translations.md#readme)
    - [WIP - Rate Limiting](./rate-limiting.md#readme)
    - [WIP - Lists](./lists.md#readme)
    - [WIP - Joke Submissions](./joke-submissions.md#readme)
    - [WIP - Joke Caching](./joke-caching.md#readme)
    - [Legacy / Deprecated Features](./legacy-features.md#readme)



<br><br><br>
<!-- #MARKER Important Info -->

## Important Information:
This section contains some very important information about how this documentation works.  
It is probably vital for you to read this.

<br>

> ### Settings Notation
> In this documentation you'll encounter a lot of values denoted like this: `settings.foo.bar`  
> These values are defined at a central point for easy modification. You'll find them in the JSON-like `settings` object in the file [settings.js](../..settings.js) in the root directory of JokeAPI.  
> The settings object can not be modified at runtime due to the usage of `Object.freeze()` - this prevents possible XSS-like exploits and just general inconsistencies.




<br><br><br>
<!-- #MARKER knowledge prerequisites -->

## Knowledge Prerequisites:
These are the requirements you need to know in order to understand or work with JokeAPI's code.

<br>

### Important requirements:
The more of these things you know, the better.
- JavaScript
    - Extensive knowledge of JS is required as a lot of very complex syntax is used
    - Promise API (including `Promise.all()`)
- Node.js
    - Native modules
        - path   (especially `resolve()` and `join()`)
        - stream (how to create and pipe streams)
        - fs     (reading, writing files, creating Read- and WriteStreams)
        - http   (request methods, accepting and parsing requests, piping Read- and WriteStreams to the client)
- HTTP
    - Using reverse proxies (especially proxy headers like "X-Forwarded-For")
    - Request methods
    - Response headers
    - Encoding
- JSON
    - Reading JSON files
    - Writing JSON files
    - Parsing JSON and ensuring correct format

<br>

### Optional:
These are **optional** requirements. It is helpful but not necessary to know them.
- SQL (simple syntax - SELECT, WHERE, INSERT INTO, ...)
- HTML / CSS / Web-JS (for modifying the docs)
- SvCoreLib (my own core library used extensively throughout the API. It's pretty well documented [here](https://github.com/Sv443/SvCoreLib/blob/master/docs.md#readme))



<br><br><br>
<!-- #MARKER technical prerequisites -->

## Technical Prerequisites:
These are the technical requirements you need to have in order to work with JokeAPI's code.

### Required:
You **need** these things for working on JokeAPI.
- Node.js v11.7.0 or newer (needed for the Brotli compression of the docs - otherwise set `settings.httpServer.encodings.brotli` to `false`)
- MySQL / MariaDB / MSSQL database with a UTF-8 collated database that has the name defined in `settings.sql.database` (usually `jokeapi`)

### Optional:
These things are **optional** but strongly recommended.
- Visual Studio Code with the following extensions (JokeAPI has custom support for them):
    - [`fabiospampinato.vscode-highlight`](https://marketplace.visualstudio.com/items?itemName=fabiospampinato.vscode-highlight)
    - [`coenraads.bracket-pair-colorizer-2`](https://marketplace.visualstudio.com/items?itemName=coenraads.bracket-pair-colorizer-2)



<br><br><br>

<!-- #MARKER Misc Concepts -->

## Miscellaneous Concepts:
These are some miscellaneous concepts that I didn't feel like creating a separate file for.  
You will probably get redirected to this section by the other files in this documentation.

<br>

> ### Category Aliases:
> Category aliases were introduced when I really started to dislike the category name `Miscellaneous`, which I wanted to change to `Misc`  
> In order not to break backwards compatibility though, `Miscellaneous` would have to still work.  
> So I decided to kill two birds with one stone by implementing category aliases.  
> Internally, they are resolved to one of the primary categories.  
> Externally, they provide a synonymous category name that you can use if you don't like the default one.  
>   
> Example: The category `Miscellaneous` will be automatically converted to `Misc` by JokeAPI and will be treated as if the client used `Misc` in the first place.

<br>

> ### Filter Components:
> The filter components are all of the parameters that can be set to filter out jokes.  
> As of v2.4.0 there are these filter components:  
> | Component | Defined in / settings node |
> | --- | --- |
> | Joke Category | `settings.jokes.possible.categories` |
> | Category Aliases | `settings.jokes.possible.categoryAliases` |
> | (Blacklist-) Flags | `settings.jokes.possible.flags` |
> | (Response) Formats | `settings.jokes.possible.formats` |
> | Joke Types | `settings.jokes.possible.types` |
> | Joke Language | File at `settings.languages.langFilePath` |
> | ID Range | Joke files - amount of items in `jokes` array |



<br><br><br>

**> EOF, please see the other topics in the [table of contents](#table-of-contents) <**


<br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br> <!-- padding to improve the #anchor links at the bottom -->