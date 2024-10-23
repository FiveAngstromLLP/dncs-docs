# Parser

This module provides tools to model polymers, particularly focusing on amino acid sequences and force fields for molecular simulations. It offers functions to generate polymer structures from sequences, convert between formats (such as PDB), and parse force field data for use in simulations.

## Overview

### Key Components:
1. **Data Structures**: These structures represent atoms, bonds, dihedrals, monomers, polymers, and energy parameters.
2. **Force Field Handling**: Provides support for initializing force fields used in molecular simulations.l
3. **Sequence Generation**: Functions to generate polymer structures from amino acid sequences.
4. **File Parsing**: Functions to read and convert PDB files into internal representations.
5. **Utilities**: Helper functions to manage and manipulate atoms and sequences.

## Data Structures

### Atom
Represents a single atom within a polymer, including its serial number, name, residue information, position, and properties like charge, mass, and atomic velocities. Each atom can also store force field-related parameters such as Lennard-Jones coefficients.

**Methods**:
- **`new(line: String)`**: Constructs an atom from a line of PDB text, reading its attributes such as position, charge, and element.

### Bond
Models the interaction between two atoms. It tracks the identities of both atoms that are bonded together.

### Dihedral
Represents a dihedral angle formed by four atoms in sequence. Dihedrals are critical in molecular simulations to define the rotation about a bond.

### Energy
Stores energy-related parameters for an atom type, such as Lennard-Jones sigma and epsilon values, which are used in force field calculations.

### Monomer
Defines a monomer unit (such as an amino acid) within a polymer. It contains information about the monomer's identity, the atoms it contains, and other structural data.

### Polymer
Represents a polymer chain composed of multiple monomer units. It allows for easy manipulation of the entire polymer as a sequence of monomers.

### Force Field
Defines the force field used for molecular simulations. Force fields include parameters like atomic interactions, bond forces, torsional angles, and non-bonded forces.

## Force Field Handling

### `FF` Enum
Enumerates the supported force fields, including several variants of the AMBER force field.

**Methods**:
- **`init()`**: Initializes and returns a `ForceField` struct by parsing the associated force field files.

## Sequence Generation

### **`generate(seq: &str)`**
Generates a polymer structure from a given amino acid sequence. This function takes an amino acid sequence as input (using single-letter codes) and returns a vector of atom structures representing the polymer.

**Process**:
- Validates the sequence for correct amino acid codes.
- Adds appropriate atoms for N- and C-terminal groups.
- Iteratively builds the polymer by adding monomer units based on the sequence.

### **`atoms_to_pdbstring(atoms: Vec<Atom>)`**
Converts a list of atoms into a PDB-formatted string. This is useful for exporting the structure of a polymer for visualization or further processing.

**Process**:
- Filters out atoms that don't belong to the main chain (e.g., terminal atoms).
- Formats each atom according to the PDB standard.

### **`pdb_to_atoms(pdb_string: &str)`**
Parses a PDB file and converts it into a list of atoms. This function reads PDB content and creates atom representations for each line labeled as "ATOM" or "HETATM".

### **`atoms_to_seq(atoms: Vec<Atom>)`**
Converts a list of atoms back into an amino acid sequence using single-letter codes. It detects changes in residue numbers and builds the corresponding sequence.

## Utilities

### Data Loading
The module uses lazy initialization to load static data structures (e.g., amino acid monomers, bond connections, and dihedral angles) from JSON files.

### Atom Debug Formatting
Implements custom formatting for atoms to facilitate easy printing and debugging.

## Usage Examples

### 1. **Generating a Polymer from a Sequence**

```rust
let sequence = "ACDEFGHIKLMNPQRSTVWY";
let atoms = generate(sequence);
```

### 2. **Converting Atoms to PDB Format**

```rust
let pdb_string = atoms_to_pdbstring(atoms);
println!("{}", pdb_string);
```

### 3. **Parsing a PDB File**

```rust
let pdb_content = std::fs::read_to_string("path/to/file.pdb").expect("Failed to read PDB file");
let atoms = pdb_to_atoms(&pdb_content);
```

### 4. **Converting Atoms to an Amino Acid Sequence**

```rust
let sequence = atoms_to_seq(atoms);
println!("Amino Acid Sequence: {}", sequence);
```

### 5. **Initializing a Force Field**

```rust
let force_field = FF::AMBER99SB.init();
```

## Notes

- **Error Handling**: The module relies on `unwrap()` for certain operations, which may cause panics if data files are missing or corrupted. For production environments, it's recommended to implement more robust error handling.
- **Data Files**: The module depends on specific data files located in the `data` directory. These files include information on atoms, bonds, dihedrals, and energy parameters.
- **Sequence Validation**: The `generate` function assumes the provided sequence is valid, and checks that the sequence doesn't contain invalid characters like `B`, `O`, `J`, `U`, `X`, or `Z`.
