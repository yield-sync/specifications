# Rules

## Smart Contract Layout & Line Ordering

### Variables

1. Type (`address`, `bytes`, etc.)
	2. Visibility (`public` | `private` | `internal` | `external`)
		3. Array

### Mapping

#### Line Ordering
1. Visibility (`public` | `private` | `internal` | `external`)
	2. Type (`address`, `bytes`, etc.)
		3. Struct

#### Getters
1. If the mapping consists strictly of primative types than the visibility must be set to `public` otherwise a getter function be defined

### Function

1. Interface Implementation
	2. Visibility (`public` | `private` | `internal` | `external`)
		3. State Interaction (`pure` | `view`)
			4. Restriction (`Access Control` etc. DEFAULT_ADMIN_ROLE first)
				5. Complexity (Calls to inherited functions, external functions, change state)
					6. Alphabetical 
