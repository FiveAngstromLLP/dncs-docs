# Generating Polymers

The `generate` function is the core functionality of this library. It takes an amino acid sequence as input and returns a vector of `Atom` structs representing the polymer structure.

## Function Signature

```rust
pub fn generate(seq: &str) -> Vec<Atom>
```

## Usage Example

```rust
use dncs::polygen;

let sequence = "ACDEFGHIKLMNPQRSTVWY";
let polymer = polygen::generate(sequence);
println!("Generated polymer with {} atoms", polymer.len());
```

## Notes

- The input sequence should only contain valid amino acid codes.
- The function handles both N-terminal and C-terminal special cases.
- It alternates between two sets of coordinates for different conformations in the polymer chain.
