# Simple Circuit

- `simple_circuit.json` is the compiled circuit with bytecodes.
- `simple_circuit.gz` is the generated witness from the circuit.
- `Prover.toml` is the input values for the circuit.

### Check the circuit for syntax errors

```bash
nargo check
```

### Execute the circuit and generate the witness using the values in `Prover.toml`

```bash
nargo execute
```

### Generate Proof using the witness

```bash
bb prove -b ./target/simple_circuit.json -w ./target/simple_circuit.gz -o ./target
```

### Generate VK

```bash
bb write_vk -b ./target/simple_circuit.json -o ./target
```

### References

[Noir Quick Start](https://noir-lang.org/docs/getting_started/quick_start)
