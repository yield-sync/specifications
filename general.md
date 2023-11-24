# Development

## Smart Contract Layout

### Naming Conventions

1. All internal variables must begin with `_`
2. All parameters of functions must begin with `_`
3. All `constant` and `immutable` variables must be capitalized snake-case
4. All return variable names must appended with a `_`
	1. Good -> `returns (uint256 value_)`
	2. Bad -> `returns (uint256 value)`

### Getters

#### General

1. The Getter function should be the name of the internal variable or mapping without the prepended `_`
2. The return type on a mapping getter should have a follow-up variable name
	1. Good -> `returns (uint256 value_)`
	2. Bad -> `returns (uint256)`

### Primative Types

#### Ordering

1. Mutability -> `constant` | `immutable` | `*`
2. Visibility -> `public` | `private` | `internal` | `external`
3. Type -> (Alphabetical) `address` | `bytes` | `uint256`
4. Non-Array than Array
5. Alphabetical

### Mappings

#### Ordering

1. Mutability -> `constant` | `immutable` | `*`
2. Visibility -> `public` | `private` | `internal` | `external`
3. Type -> (Alphabetical) `address` | `bytes` | `Struct`
4. mapping with only primitive types comes first
5. Non-Array than Array
6. Alphabetical

#### Mapping Getters

1. The Getter function is to be defined only if the mapping consists of non-primitive types otherwise visibility is `public` 

### Functions

#### Ordering

1. Group by interface implementation
2. Visibility -> `public` | `private` | `internal` | `external`
3. State interaction -> `pure` | `view`
4. Modifiers such as restrictions (ex: `Access Control`)
	1. No modifier
	2. Modifer Alphabetical
5. Function Name Alphabetical
6. Parameters
	1. count
	2. parameter type name
