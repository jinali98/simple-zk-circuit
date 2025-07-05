# Simple Circuit

A Noir-based zero-knowledge circuit implementation for proof generation and verification.

## Overview

This project demonstrates a simple zero-knowledge circuit using the Noir programming language. The circuit can generate proofs that can be verified both on-chain and off-chain.

## Project Structure

The project contains the following key files:

- `simple_circuit.json` - The compiled circuit with bytecodes
- `simple_circuit.gz` - The generated witness from the circuit
- `Prover.toml` - Input values for the circuit
- `src/main.nr` - The main circuit implementation

## Usage

### 1. Check Circuit Syntax

Verify that the circuit has no syntax errors:

```bash
nargo check
```

### 2. Execute Circuit and Generate Witness

Execute the circuit using the input values defined in `Prover.toml`:

```bash
nargo execute
```

### 3. Generate Proof

Generate a zero-knowledge proof using the witness:

```bash
bb prove -b ./target/simple_circuit.json -w ./target/simple_circuit.gz -o ./target
```

### 4. Generate Verification Key (VK)

Create a verification key for proof verification:

```bash
bb write_vk -b ./target/simple_circuit.json -o ./target
```

## Proof Verification

Proof verification can be performed both on-chain and off-chain:

- **On-chain**: The proof file can be read in byte format and submitted to a verifier smart contract for verification
- **Off-chain**: Proofs can be verified using the generated verification key

## References

- [Noir Quick Start Guide](https://noir-lang.org/docs/getting_started/quick_start)
- [Noir Documentation](https://noir-lang.org/docs)



## What is a Verification Key?

A verification key (VK) is a **public parameter** that allows anyone to verify a zero-knowledge proof without needing to know the private inputs that were used to generate it. It's essentially the "public key" for verifying proofs.

### How Verification Keys Work

1. **Circuit Compilation**: When you compile a circuit (like your `simple_circuit.json`), the system generates two keys:

   - **Proving Key (PK)**: Used to generate proofs (kept private)
   - **Verification Key (VK)**: Used to verify proofs (can be shared publicly)

2. **Proof Generation**: Using the proving key and private inputs, you generate a proof that demonstrates you know some secret information without revealing it.

3. **Proof Verification**: Anyone with the verification key can verify that the proof is valid without learning the private inputs.

### Why Verification Keys Are Important

- **Security**: The VK is deterministic - it's the same for all proofs from the same circuit
- **Efficiency**: Verification is much faster than proof generation
- **Privacy**: The VK doesn't reveal any information about the private inputs
- **Scalability**: One VK can verify many different proofs from the same circuit
