# babel-helper-module-imports

## WARNING
This helper is **DEPRECATED** in favor of `addImport` method of file, compatible
with `extractDynamicImports` option of babel-core.
Eventually, it will be merged into babel-core and will not be available for
other plugins and helpers.

## Installation

```sh
npm install babel-helper-module-imports --save
```

## Usage

### `import "source"`

```js
import { addSideEffect } from "babel-helper-module-imports";
addSideEffect(path, 'source');
```

### `import { named } from "source"`

```js
import { addNamed } from "babel-helper-module-imports";
addNamed(path, 'named', 'source');
```

### `import { named as _hintedName } from "source"`

```js
import { addNamed } from "babel-helper-module-imports";
addNamed(path, 'named', 'source', { nameHint: "hintedName" });
```

### `import _default from "source"`

```js
import { addDefault } from "babel-helper-module-imports";
addDefault(path, 'source');
```

### `import hintedName from "source"`

```js
import { addDefault } from "babel-helper-module-imports";
addDefault(path, 'source', { nameHint: "hintedName" })
```

### `import * as _namespace from "source"`

```js
import { addNamespace } from "babel-helper-module-imports";
addNamespace(path, 'source');
```

## Examples

### Adding a named import

```js
import { addNamed } from "babel-helper-module-imports";

export default function({ types: t }) {
  return {
    visitor: {
      ReferencedIdentifier(path) {
        let importName = this.importName;
        if (importName) {
          importName = t.cloneDeep(importName);
        } else {
          // require('bluebird').coroutine
          importName = this.importName = addNamed(path, 'coroutine', 'bluebird');
        }

        path.replaceWith(importName);
      }
    },
  };
}
```
