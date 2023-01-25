This is the code for the Hadamard gate simulation at the end of chapter 1:
```python
# Installing qiskit
!pip install qiskit# Performing the imports
from qiskit import QuantumCircuit, assemble, Aer
from qiskit.visualization import plot_histogram
# Creating the quantum circuit and applying a Hadamard gate.
qc = QuantumCircuit(1)
qc.h(0)
# Drawing the circuit
qc.draw()
# Creating the backend for the circuit using Aer.
sim = Aer.get_backend('aer_simulator') 
# Measures the qubit in the circuit.
qc.measure_all()
# Converts the circuit object into a format that the simulator can understand and execute.
qobj = assemble(qc)
# Gets the counts of each outcome and prints a histogram of that.
results = sim.run(qobj).result().get_counts()
plot_histogram(results)
```
