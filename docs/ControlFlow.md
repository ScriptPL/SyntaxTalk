# Control Flow

### Imports and Package Managing

Keeping minimalist standarts, the only keyword for importats is `use` which is followed by a string literal tracking the name of the package or file. The Lexer automatically scans for the keyword and starts lexing packages before the entry file is finished lexing.

```
# Import Libraries
use 'html', 'ecs', 'stdlib'

# Import your own files
use 'path/to/file.scriptpl'

# Import 3rd party
use 'www.link-to-repo.com/path/to/.git'
```
