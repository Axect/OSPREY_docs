# Chapter 1: PBH (Primordial Black Hole)

Welcome to the OSPREY tutorial! OSPREY is a tool designed to simulate the particles emitted by **Primordial Black Holes (PBHs)** through a process called Hawking radiation. In this first chapter, we'll dive into the very core concept: the PBH itself.

## What's the Big Idea? Meet the PBH

Imagine you want to study the faint signals coming from tiny black holes that might have formed just moments after the Big Bang. These are Primordial Black Holes. They aren't like the giant black holes at the center of galaxies; they can be much, much smaller.

The big idea in OSPREY is that everything starts with the PBH. Think of it like the **engine** of our simulation. Just like a car's engine burns fuel to produce power, a PBH "radiates" particles based on its fundamental property: its **mass**.

**Our Goal:** We want to represent a PBH in our code so we can later calculate what kinds of particles it emits and how energetic they are.

## What is a PBH in OSPREY?

In OSPREY, we have a specific code structure (called a `struct` in Rust) named `PBH` to represent a Primordial Black Hole. It's surprisingly simple! Its main job is to hold onto one crucial piece of information:

*   **Mass:** How heavy the PBH is (usually measured in grams).

Why is mass so important? Because in the world of theoretical physics (specifically, Hawking radiation), the mass of a black hole determines almost everything about it: its size, its temperature, and what particles it emits. A lighter PBH is hotter and radiates more intensely than a heavier one!

## How to Create a PBH in OSPREY

Let's say we want to simulate a PBH with a mass of 1 quadrillion grams (that's 1 followed by 15 zeros, or `1e15` in scientific notation). Here's how you create the `PBH` object in your code:

```rust
// Import the PBH structure from the osprey library
use primary::core::PBH; // Assuming PBH is in osprey::primary::core

// Define the mass (in grams)
let pbh_mass_grams = 1e15; // 10^15 g

// Create a new PBH instance
let my_pbh = PBH::new(pbh_mass_grams);

// Now, 'my_pbh' holds our PBH object!
println!("Created a PBH with mass: {} g", my_pbh.mass);
```

**Explanation:**

1.  `use primary::core::PBH;`: This line tells Rust where to find the definition of `PBH`.
2.  `let pbh_mass_grams = 1e15;`: We store our desired mass in a variable. Using `1e15` is a common way to write large numbers like 1,000,000,000,000,000.
3.  `let my_pbh = PBH::new(pbh_mass_grams);`: This is the key step! We call the `new` function associated with `PBH`, passing in the mass. This function creates the actual `PBH` object.
4.  `println!(...)`: We print the mass stored inside our new `my_pbh` object just to confirm it worked.

**Input:** The mass of the PBH (e.g., `1e15` grams).
**Output:** A `PBH` object stored in the `my_pbh` variable, ready for further calculations.

That's it! You've just defined the central object of our simulation.

## Under the Hood: What Happens When You Call `PBH::new`?

When you call `PBH::new(mass)`, the process is very straightforward:

1.  **Input:** You provide the `mass` value (a number representing grams).
2.  **Storage:** The `PBH::new` function takes that mass value and stores it inside a new `PBH` structure.
3.  **Output:** The function returns this newly created `PBH` structure, which now holds the mass you provided.

Let's look at the actual code definition (simplified):

**File:** `primary/src/core.rs`

```rust
/// Represents a Schwarzschild (non-spinning) Primordial Black Hole.
pub struct PBH {
    /// Mass of the Primordial Black Hole (in grams, g).
    pub mass: f64, // f64 means a standard 64-bit floating-point number
}

impl PBH {
    /// Creates a new PBH instance.
    /// # Arguments
    /// * `mass` - Mass of the PBH in grams (g).
    pub fn new(mass: f64) -> Self {
        // Just create a PBH struct, putting the provided mass
        // into the 'mass' field.
        PBH { mass }
    }

    // ... other methods like temperature() and emission_rate() exist here ...
    // We will cover them later!
}
```

**Explanation:**

*   `pub struct PBH { ... }`: This defines the `PBH` structure. It only contains one piece of data: `pub mass: f64`, which holds the mass as a number.
*   `impl PBH { ... }`: This block contains functions (called "methods") associated with the `PBH` structure.
*   `pub fn new(mass: f64) -> Self`: This defines the `new` function. It takes one argument `mass` (a number) and returns `Self` (which means it returns an object of type `PBH`).
*   `PBH { mass }`: This is the core logic. It creates a `PBH` instance and sets its internal `mass` field to the value passed into the function.

## What Can We Do With a PBH Object?

Once you have a `PBH` object, you can use it to calculate its properties. For example, you can find its **Hawking Temperature**:

```rust
// (Assuming my_pbh was created as shown before)

// Calculate the Hawking temperature
let temperature_mev = my_pbh.temperature(); // Returns temperature in Mega-electron Volts (MeV)

println!("PBH Temperature: {:.2} MeV", temperature_mev);
```

**Explanation:**

*   `my_pbh.temperature()`: We call the `temperature` method on our `PBH` object. This method uses the stored `mass` to calculate the temperature based on physics formulas.

The most important calculation is finding the **rate at which the PBH emits different kinds of particles**. This involves another method called `emission_rate`. It needs the `PBH` object, the type of [Particle / StandardModel](02_particle___standardmodel_.md) we're interested in, and a range of energies. It also uses something called [GreyBody Factors](03_greybody_factors__greybody___greybodydata___greybodyfit__.md) behind the scenes.

```rust
// This is just a sneak peek - we'll cover this in detail later!
// let energies = vec![...]; // Define some energy values
// let photon = StandardModel::Photon; // Choose a particle type
// let photon_emission_rate = my_pbh.emission_rate(photon, &energies);
```

We won't dive deep into `emission_rate` right now, as it's covered in detail in [Chapter 4: Emission Rate Calculation (PBH::emission_rate)](04_emission_rate_calculation__pbh__emission_rate__.md). For now, just remember that the `PBH` object you created is the essential starting point for all these calculations.

## Conclusion

In this chapter, we met the star of our show: the Primordial Black Hole, represented by the `PBH` struct in OSPREY. We learned that:

*   The PBH is the central "engine" of the simulation, the source of particles.
*   Its most important property is its **mass**.
*   Creating a `PBH` object is simple: `PBH::new(mass_in_grams)`.
*   This `PBH` object holds the mass and allows us to calculate other properties like temperature and particle emission rates (which we'll explore soon).

Now that we have our source object (the PBH), the next logical step is to understand *what* it can emit. In the next chapter, we'll explore the different types of particles in the Standard Model that PBHs can radiate.

Let's move on to [Chapter 2: Particle / StandardModel](02_particle___standardmodel_.md)!

---

Generated by [AI Codebase Knowledge Builder](https://github.com/The-Pocket/Tutorial-Codebase-Knowledge)