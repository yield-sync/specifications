# Development

## Smart Contract Layout & Line Ordering

### Variables

1. Type (`address`, `bytes`, etc.)
2. Visibility (`public` | `private` | `internal` | `external`)
3. Array

### Mappings

#### Line Ordering

1. Visibility (`public` | `private` | `internal` | `external`)
2. Type (`address`, `bytes`, etc.)
3. Struct

#### Getters

1. If the mapping consists strictly of primative types than the visibility must be set to `public` otherwise a getter function be defined.
2. If a getter function is necessary, than the internal mapping must be prepended with a `_`.

### Function

1. Group by interface implementation
2. Visibility (`public` | `private` | `internal` | `external`)
3. State interaction (`pure` | `view`)
4. Modifiers such as restrictions (ex: `Access Control`)
	1. Modifer Alphabetical
	2. Functional Alphabetical
5. Complexity (Calls to inherited functions, external functions, change state)
6. Alphabetical
