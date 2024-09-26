# Writing PDB Files

The `to_pdb` function in our library provides an easy way to write your generated polymer structure to a PDB (Protein Data Bank) file. This function takes a vector of `Atom` structs and a filename as input, and creates a PDB file with the specified name.

## Function Signature

```rust
pub fn to_pdb(polymer: &Vec<Atom>, filename: &str) -> Result<(), std::io::Error>
```

## Usage Example

Here's a simple example of how to use the `to_pdb` function:

```rust
use dncs::polygen;

let sequence = "ACDEFGHIKLMNPQRSTVWY";
let polymer = polygen::generate(sequence);

match polygen::to_pdb(&polymer, "output.pdb") {
    Ok(_) => println!("PDB file written successfully"),
    Err(e) => eprintln!("Error writing PDB file: {}", e),
}
```

This will create a file named `output.pdb` in your current directory, containing the PDB-formatted representation of your polymer structure.

## PDB File Format

The generated PDB file follows the standard PDB format, with each line representing an atom in the structure. The format includes information such as atom serial number, atom name, residue name, chain identifier, residue sequence number, and 3D coordinates.

## Error Handling

The `to_pdb` function returns a `Result` type, allowing you to handle any potential I/O errors that might occur during file writing. It's good practice to handle these errors appropriately in your application.

Remember to include proper error handling in your code when using this function, especially in production environments where file I/O operations might fail due to various reasons like insufficient permissions or disk space.
