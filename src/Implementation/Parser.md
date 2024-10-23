## Parser

This module provides tools to model polymers, particularly focusing on amino acid sequences and force fields for molecular simulations. It offers functions to generate polymer structures from sequences, convert between formats (such as PDB), and parse force field data for use in simulations.

### Data Structures

- **Atom**: Represents a single atom within a polymer, including its serial number, name, residue information, position, and properties like charge, mass, and atomic velocities. Each atom can also store force field-related parameters such as Lennard-Jones coefficients.

- **Bond**: Models the interaction between two atoms. It tracks the identities of both atoms that are bonded together.

- **Dihedral**: Represents a dihedral angle formed by four atoms in sequence. Dihedrals are critical in molecular simulations to define the rotation about a bond.

- **Energy**: Stores energy-related parameters for an atom type, such as Lennard-Jones sigma and epsilon values, which are used in force field calculations.

- **Monomer**: Defines a monomer unit (such as an amino acid) within a polymer. It contains information about the monomer's identity, the atoms it contains, and other structural data.

- **Polymer**: Represents a polymer chain composed of multiple monomer units. It allows for easy manipulation of the entire polymer as a sequence of monomers.

- **Force Field**: Defines the force field used for molecular simulations. Force fields include parameters like atomic interactions, bond forces, torsional angles, and non-bonded forces.

### Force Field Handling

- **FF** Enum
  Enumerates the supported force fields, including several variants of the AMBER force field.
  ```rs
  enum FF {
    AMBER03,
    AMBER10,
    AMBER96,
    AMBER99SB,
    AMBERFB15,
  }
  ```
  **Methods**:
  - **`init()`**: Initializes and returns a `ForceField` struct by parsing the associated force field files.

### Function

- **`generate(seq: &str)`**
  Generates a polymer structure from a given amino acid sequence. This function takes an amino acid sequence as input (using single-letter codes) and returns a vector of atom structures representing the polymer.

  **Process**:
  - Validates the sequence for correct amino acid codes.
  - Adds appropriate atoms for N- and C-terminal groups.
  - Iteratively builds the polymer by adding monomer units based on the sequence.

- **`atoms_to_pdbstring(atoms: Vec<Atom>)`**
  Converts a list of atoms into a PDB-formatted string. This is useful for exporting the structure of a polymer for visualization or further processing.

  **Process**:
  - Filters out atoms that don't belong to the main chain (e.g., terminal atoms).
  - Formats each atom according to the PDB standard.

- **`pdb_to_atoms(pdb_string: &str)`**
  Parses a PDB file and converts it into a list of atoms. This function reads PDB content and creates atom representations for each line labeled as "ATOM" or "HETATM".

## Example

- **Generate Polymer**

  ```rs
  extern crate libdncs;
  use libdncs::parser::generate;

  fn main(){
      let atoms = generate("ACDEFGHIKLMNPQRSTVWY"); // PROTEIN SEQUENCE
      for atom in atoms.iter() {
          println!("{:?}", atom)
      }
  }
  ```
