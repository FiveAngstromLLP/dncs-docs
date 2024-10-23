
## Amber

The `Amber` struct is designed to model a molecular system using the Amber force field, which is extensively applied in molecular dynamics simulations. Below are its properties and methods, with mathematical representations included for clarity.

### Fields
- **system**: An instance of the `System` struct that encapsulates information about the particles in the system and their interaction parameters.

### Methods

- **`new(system: System) -> Self`**
  - **Description**: Constructs a new instance of the `Amber` struct using the provided `System`.
  - **Parameters**:
    - `system`: An instance of the `System` struct containing the particles and their interaction properties.
  - **Returns**: A new instance of `Amber`.

- **`energy(&self) -> f64`**
  - **Description**: Computes the total energy of the molecular system, including contributions from various interactions.

    \\[
    E_{\text{total}} = E_{\text{non-bonded}} + E_{\text{bonds}} + E_{\text{angles}} + E_{\text{torsions}} + E_{\text{hydrogen bonds}}
    \\]
  - **Returns**: The total energy in kilocalories per mole (kcal/mol).

- **`nonbonded_energy(&self, iatom: &Atom) -> f64`**
  - **Description**: Computes the non-bonded energy contribution for a specific atom, including Lennard-Jones and electrostatic interactions.

    \\[
    E_{\text{non-bonded}} = \sum_{j \neq i} \left( E_{\text{LJ}}(i, j) + E_{\text{electrostatic}}(i, j) \right)
    \\]
  - **Parameters**:
    - `iatom`: A reference to the `Atom` for which the non-bonded energy is being calculated.
  - **Returns**: The non-bonded energy contribution in units of kg·Å²/s².

- **`harmonic_bond_force(&self, iatom: &Atom) -> f64`**
  - **Description**: Calculates the harmonic bond energy associated with the given atom based on its bonded neighbors.

    \\[
    E_{\text{bond}} = \frac{1}{2} k (r - r_0)^2
    \\]
    where \\( k \\) is the bond force constant, \\( r \\) is the current bond length, and \\( r_0 \\) is the equilibrium bond length.
  - **Parameters**:
    - `iatom`: A reference to the `Atom` for which the bond force is being calculated.
  - **Returns**: The harmonic bond energy in units of kcal/mol.

- **`harmonic_angle_force(&self, iatom: &Atom) -> f64`**
  - **Description**: Computes the harmonic angle energy associated with the given atom based on its bonded neighbors.

    \\[
    E_{\text{angle}} = \frac{1}{2} k_{\theta} (\theta - \theta_0)^2
    \\]
    where \\( k_{\theta} \\) is the angle force constant, \\( \theta \\) is the current angle, and \\( \theta_0 \\) is the equilibrium angle.
  - **Parameters**:
    - `iatom`: A reference to the `Atom` for which the angle force is calculated.
  - **Returns**: The harmonic angle energy in units of kcal/mol.

- **`periodic_torsional_force(&self) -> f64`**
  - **Description**: Calculates the energy contributions from periodic torsional interactions in the system.

    \\[
    E_{\text{torsion}} = \sum_{n} \frac{1}{2} k_n (1 + \cos(n \phi - \gamma))
    \\]
    where \\( V_n \\) is the torsional force constant, \\( n \\) is the periodicity, \\( \phi \\) is the torsion angle, and \\( \gamma \\) is the phase.
  - **Returns**: The total periodic torsional energy in kcal/mol.

- **`hydrogen_bond_energy(&self) -> f64`**
  - **Description**: Computes the total energy associated with hydrogen bonds in the system.

  - **Returns**: The total hydrogen bond energy in kcal/mol.

- **`lennard_jones_energy(i: &Atom, j: &Atom) -> f64`**
  - **Description**: Calculates the Lennard-Jones potential energy between two atoms.

    \\[
    E_{\text{LJ}}(i, j) = 4\epsilon \left( \left( \frac{\sigma}{r} \right)^{12} - \left( \frac{\sigma}{r} \right)^{6} \right)
    \\]
    where \\( r \\) is the distance between atoms \\( i \\) and \\( j \\), \\( \epsilon \\) is the depth of the potential well, and \\( \sigma \\) is the finite distance at which the potential is zero.
  - **Parameters**:
    - `i`: A reference to the first `Atom`.
    - `j`: A reference to the second `Atom`.
  - **Returns**: The Lennard-Jones energy in units of kg·Å²/s².

- **`electrostatic_energy(i: &Atom, j: &Atom) -> f64`**
  - **Description**: Calculates the electrostatic potential energy between two atoms based on their charges.

    \\[
    E_{\text{electrostatic}}(i, j) = \frac{k_e \cdot q_i \cdot q_j}{r}
    \\]
    where \\( k_e \\) is Coulomb's constant, \\( q_i \\) and \\( q_j \\) are the charges of atoms \\( i \\) and \\( j \\), and \\( r \\) is the distance between the two atoms.
  - **Parameters**:
    - `i`: A reference to the first `Atom`.
    - `j`: A reference to the second `Atom`.
  - **Returns**: The electrostatic energy in units of kg·Å²/s².

- **`angle(i: &Atom, j: &Atom, k: &Atom) -> f64`**
  - **Description**: Calculates the angle formed by three atoms in degrees.

    \\[
    \theta = \arccos \left( \frac{\vec{b} \cdot \vec{c}}{|\vec{b}| |\vec{c}|} \right)
    \\]
    where \\( \vec{b} \\) and \\( \vec{c} \\) are vectors formed by the positions of the atoms.
  - **Parameters**:
    - `i`: A reference to the first `Atom`.
    - `j`: A reference to the second `Atom`.
    - `k`: A reference to the third `Atom`.
  - **Returns**: The angle in degrees.

- **`distance(i: &Atom, j: &Atom) -> f64`**
  - **Description**: Computes the Euclidean distance between two atoms.

    \\[
    d = \sqrt{(x_j - x_i)^2 + (y_j - y_i)^2 + (z_j - z_i)^2}
    \\]
  - **Parameters**:
    - `i`: A reference to the first `Atom`.
    - `j`: A reference to the second `Atom`.
  - **Returns**: The distance in angstroms (Å).
