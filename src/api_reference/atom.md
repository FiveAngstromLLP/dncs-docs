# Atom Struct

The `Atom` struct represents an individual atom in a molecular structure. It contains all the necessary information to define an atom's properties and position within a polymer.

## Fields

- `record`: String - The record type (e.g., "ATOM", "HETATM")
- `serial`: usize - Atom serial number
- `name`: String - Atom name
- `residue`: String - Residue name
- `sequence`: usize - Residue sequence number
- `x`: f64 - X coordinate
- `y`: f64 - Y coordinate
- `z`: f64 - Z coordinate
- `occupancy`: f32 - Occupancy
- `bfactor`: f32 - Temperature factor
- `element`: String - Element symbol

## Usage

The `Atom` struct is primarily used internally by the `generate` function to create polymer structures. However, you can also create `Atom` instances manually if needed:

```rust
let atom = Atom {
    record: String::from("ATOM"),
    serial: 1,
    name: String::from("N"),
    residue: String::from("ALA"),
    sequence: 1,
    x: 0.0,
    y: 0.0,
    z: 0.0,
    occupancy: 1.0,
    bfactor: 0.0,
    element: String::from("N"),
};
```

The `Debug` implementation for `Atom` allows for easy printing in PDB format:

```rust
println!("{:?}", atom);
```

This will output the atom information in a format compatible with PDB files.
