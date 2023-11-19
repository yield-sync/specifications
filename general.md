# Development

## Smart Contract Layout

### Naming Conventions

1. All internal variables must begin with `_`
2. All `constant` and `immutable` variables must be capitalized snake-case
3. All return variable names must appended with a `_`
	1. Good -> `returns (uint256 value_)`
	2. Bad -> `returns (uint256 value)`

### Getters

#### General

1. Getter function should be the name of the internal variable or mapping without the prepended `_`
2. The return type on a mapping getters should have a follow up variable name
	1. Good -> `returns (uint256 value_)`
	2. Bad -> `returns (uint256)`

### Variables

1. Type (`address` | `bytes` | `uint256` | custom)
2. Visibility (`public` | `private` | `internal` | `external`)
3. Mutability (`constant` | `immutable` | NA)
4. Array
5. Alphabetical

### Mappings

1. Visibility (`public` | `private` | `internal` | `external`)
	1. mapping with only primative types come first
2. Type (`address`, `bytes`, etc.)
3. Mutability (`constant` | `immutable` | NA)
4. Struct
5. Alphabetical

#### Mapping Getters

1. Getter function is to be defined only if the mapping consists of non-primative types otherwise visibility is `public` 

### Functions

1. Group by interface implementation
2. Visibility (`public` | `private` | `internal` | `external`)
3. State interaction (`pure` | `view`)
4. Modifiers such as restrictions (ex: `Access Control`)
	1. No modifier
	2. Modifer Alphabetical
5. Function Name Alphabetical
6. Parameters
	1. count
	2. parameter type name
