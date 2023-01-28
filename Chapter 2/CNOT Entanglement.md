This is the code for the CNOT entanglement at the end of chapter 2:
```python
# Installing qiskit
!pip install qiskit

# Peforming the imports
from qiskit import QuantumCircuit, QuantumRegister, ClassicalRegister, execute, Aer

# Create a quantum circuit with two qubits
qr = QuantumRegister(2)
cr = ClassicalRegister(2)
qc = QuantumCircuit(qr, cr)

# Applying a Hadamard gate to make the control qubit state in a superposition
qc.h(0)
# Apply CNOT gate with first qubit as control and second qubit as target
qc.cx(qr[0], qr[1])

# Measure the circuit
qc.measure(qr, cr)

# Execute the circuit on a simulator
simulator = Aer.get_backend('qasm_simulator')
result = execute(qc, simulator, shots=1000).result()

# Plot the resulting counts
from qiskit.visualization import plot_histogram
plot_histogram(result.get_counts(qc))
```
