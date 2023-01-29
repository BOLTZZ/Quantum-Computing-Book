This is the code for Grover's algorithm at the end of Chapter 3:

```python
# Installing qiskit
!pip install qiskit

# Peforming the imports
from qiskit import *

# Creating the oracle
oracle = QuantumCircuit(2, name= 'oracle')
# Adding the Controlled-Z gate
oracle.cz(0, 1)
# Convert the oracle to a gate.
oracle.to_gate()

# Creating the reflection operator for amplitude amplification
reflection = QuantumCircuit(2, name = 'reflection')
# Applies Hadamard to every qubit to take the superpositon state back to the original (00) state
reflection.h([0, 1])
# Create a circuit that only applies a negative phase only to the 00 state
reflection.z([0, 1])
reflection.cz(0, 1)
reflection.h([0, 1])
# Convert the reflection operator to a gate
reflection.to_gate()

# Creating the backend
simulator = Aer.get_backend('qasm_simulator')
# Creating the grover circuit (Hadamard superposition gates + oracel + reflection operator)
grover = QuantumCircuit(2, 2)
grover.h([0, 1])
grover.append(oracle, [0, 1])
grover.append(reflection, [0, 1])
grover.measure([0, 1], [0, 1])
# Draw the circuit
grover.draw()

# Execute Grover's algorithm
job = execute(grover, simulator, shots = 1)
result = job.result()
result.get_counts()
```
