# Generate Function

The `generate` function is a core component of the polymer generation module. It takes an amino acid sequence as input and produces a detailed polymer structure represented as a vector of `Atom` structs.

## Function Signature

```rust
pub fn generate(seq: &str) -> Vec<Atom>
```

## Parameters

- `seq`: A string slice containing the amino acid sequence. This should be a valid sequence of one-letter amino acid codes.

## Return Value

Returns a `Vec<Atom>` representing the generated polymer structure, where each `Atom` contains information about its position, element type, and other properties.

## Functionality

1. Validates the input sequence, ensuring it contains only valid amino acid codes.
2. Initializes the polymer structure, handling special cases for N-terminal and C-terminal ends.
3. Processes each amino acid in the sequence, alternating between two sets of coordinates (ALLAMINOMOLS_1 and ALLAMINOMOLS_2) to account for different conformations.
4. Applies positional adjustments using dummy atoms for relative positioning.
5. Handles the C-terminal end of the polymer.

## Usage Example

```rust
use dncs::polygen;

let sequence = "ACDEFGHIKLMNPQRSTVWY";
let polymer = polygen::generate(sequence);
println!("Generated polymer with {} atoms", polymer.len());
```

## Notes

- The function uses parallel processing with Rayon for improved performance on large datasets.
- It handles both N-terminal and C-terminal special cases automatically.
- The implementation ensures proper serial numbering and sequencing of atoms and residues.
