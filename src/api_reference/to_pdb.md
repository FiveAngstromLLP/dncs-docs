# To PDB Function

The `to_pdb` function is a utility provided by the library to write the generated polymer structure to a PDB (Protein Data Bank) file format. This function is crucial for visualizing and further analyzing the polymer structure using various molecular visualization tools.

## Function Signature

```rust
pub fn to_pdb(polymer: &Vec<Atom>, filename: &str) -> Result<(), std::io::Error>
```

## Parameters

- `polymer`: A reference to a vector of `Atom` structs representing the polymer structure.
- `filename`: A string slice containing the name of the output PDB file.

## Return Value

The function returns a `Result` type. If the operation is successful, it returns `Ok(())`. In case of an error (e.g., file creation or writing issues), it returns an `Err` containing the `std::io::Error`.

## Usage Example

```rust
use dncs::polygen;

let sequence = "ACDEFGHIKLMNPQRSTVWY";
let polymer = polygen::generate(sequence);

match polygen::to_pdb(&polymer, "output.pdb") {
    Ok(_) => println!("PDB file written successfully"),
    Err(e) => eprintln!("Error writing PDB file: {}", e),
}
```

## Notes

- The function creates a new file with the given filename. If a file with the same name already exists, it will be overwritten.
- Each atom in the polymer is written as a separate line in the PDB file.
- The PDB format used follows standard conventions, making it compatible with most molecular visualization software.
- Error handling is implemented, allowing the caller to handle potential I/O errors gracefully.
