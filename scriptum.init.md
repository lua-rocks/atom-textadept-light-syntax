# Scriptum

Output is in markdown.

    This document was created with this module, view the source file to see example input
    And see the raw readme.md for example output

Generate all documentation from the root directory:

```lua
local scriptum = require "scriptum"
scriptum.start()
```

Make sure you give the absolute path to the source root, and make
sure the output folder 'doc' in this example already exists in the source path, such as:

```lua
local scriptum = require "scriptum"
scriptum.start("C:/Users/me/Desktop/codebase", "doc")
```

Create a block comment with a tittle in the first line:

    --[[ Test Module
    Import and run with start()
    ~  local module = require "testmodule"
    ~  module.start()
    ]]

Tilde is used to mark a line as a code block when written in markdown.
Empty lines can be used if required as to your preference.

Create an API function entry with a comment block and one of more of:

    > name (typing) <default> [note]

and:

    < name (typing) [note]

Such as:

```lua
--[[ My function for documentation
> name (typing) [file will be created and overwritten]
> verbose (boolean) <true> [more output if true]
< success (boolean) [fail will be handled gracefully and return false]
]]
function module.startModule(name, verbose)
local success = false
-- sample code --
return success
end
```

Where:

- **name** is the parameter or return value
- optional **(typing)** such as (boolean), (number), (function), (string)
- optional **\<default\>** is the default value; if optional put \<nil\>, \<opt\> or \<\>
- optional **[note]** is any further information

Additionally, the **@** tag `can` be `used` to `automatically` unpack a simple table with key/value
pairs, _where_ each line is one pair ah a comment describing the key. This is used, for example, with
the module 'config'. The tag in that case is used as:

    @ config

The mark-up used in this file requires escape symbols to generate the outputs properly:

- Where **()** with **start** or **end** can be used to escape block comments open and close.
- And **()** with **a** is used to escape the @ symbol.
- Angled brackets are escaped with \\< and \\>

Override a _configuration_ *parameter* programmatically; insert your override values into a
new table using the matched key names:

```lua
local overrides = { codeSourceType = ".lua" }
scriptum.configuration(overrides)
```


## API

**start** (rootPath, outPath) : model

>  Start document generation
>
> &rarr; **rootPath** (string) <*""*> `path to read source code from`
> &rarr; **outPath** (string) <*"scriptum"*> `path to output to`
>
> &larr; **model** (table) `project model can be used for autocomlete in an IDE`

**configuration** (overrides\*)

> Modify the _configuration_ of this module programmatically.
>
> &rarr; *overrides* (table) `Each key is from a valid name, the value is the override`
> - codeSourceType = ".lua" `Looking for these source code files`
> - outputType = ".md" `Output file suffix`
> - rootPath = "" `Search files here`
> - outPath = "doc" `Generate output here`
>

## Project

+ [Back to root](README.md)
