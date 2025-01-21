# Quantum-Computing-The-IBM-Q-Experience-Superposition-Double-Slit-Experiment-and-Entanglement
Quantum computing has opened up new possibilities in the realm of computation. IBM's Q Experience provides a cloud-based platform for users to access real quantum computers and simulators to explore and work with quantum circuits. In this example, we will demonstrate how to create simple quantum circuits to showcase key quantum concepts, including superposition, the double-slit experiment, and entanglement using IBM Q Experience and its Qiskit framework.
Prerequisites

    IBM Q Experience account: You'll need an IBM Q Experience account to access real quantum computers via Qiskit.
    Qiskit installed: Qiskit is the open-source quantum computing framework by IBM that provides tools for working with quantum circuits.

You can install Qiskit via pip:

pip install qiskit

Quantum Concepts Demonstrated

    Superposition: In quantum computing, superposition allows quantum bits (qubits) to exist in multiple states at once, as opposed to classical bits that are either 0 or 1.
    Double-Slit Experiment: A thought experiment that demonstrates the wave-particle duality of matter and the concept of interference.
    Entanglement: A quantum phenomenon where qubits become correlated in such a way that the state of one qubit instantaneously affects the state of another, no matter the distance between them.

1. Setting up the IBM Q Experience and Qiskit

    Sign Up for IBM Q Experience:
        Go to IBM Q Experience and create an account.
        After signing up, create an API token from your IBM Q account page under Account Settings. This token will allow you to access IBM's quantum computers programmatically.

    Set up Qiskit: If you haven't installed Qiskit yet, install it via the command below:

pip install qiskit

Set up Your IBM Qiskit Account: To connect to IBM Q's cloud services, you’ll need to authenticate using your API token.

from qiskit import IBMQ

# Replace with your IBM Q API token
IBMQ.save_account('YOUR_API_TOKEN')

After saving your account, load it with:

    IBMQ.load_account()

2. Superposition: Quantum State Creation

The first demonstration is creating a superposition state, where a qubit exists in a linear combination of both the 0 and 1 states. We'll create a quantum circuit that puts a qubit in a superposition state using a Hadamard gate.

from qiskit import QuantumCircuit, Aer, execute

# Create a quantum circuit with 1 qubit
qc = QuantumCircuit(1)

# Apply Hadamard gate to create superposition
qc.h(0)

# Add a measurement to read the qubit's state
qc.measure_all()

# Simulate the quantum circuit using Aer's qasm_simulator
simulator = Aer.get_backend('qasm_simulator')

# Execute the circuit on the simulator
result = execute(qc, simulator, shots=1024).result()

# Get and plot the results
counts = result.get_counts()
print("\nResult of the superposition circuit: ", counts)

    Explanation:
        qc.h(0) applies a Hadamard gate to qubit 0, which creates a superposition of |0⟩ and |1⟩.
        qc.measure_all() measures the state of the qubit.
        The result shows a roughly equal probability of getting 0 or 1, as expected from a superposition state.

3. The Double-Slit Experiment: Interference Pattern

In quantum mechanics, the double-slit experiment demonstrates interference. We'll simulate this experiment by running multiple quantum circuits in superposition, similar to how quantum particles pass through two slits and interfere with each other.

# Create a quantum circuit with 2 qubits
qc = QuantumCircuit(2)

# Apply Hadamard gate to both qubits to create superposition
qc.h(0)
qc.h(1)

# Add a controlled-NOT (CNOT) gate to create entanglement
qc.cx(0, 1)

# Add a measurement to read the qubits' states
qc.measure_all()

# Execute the circuit on the simulator
result = execute(qc, simulator, shots=1024).result()

# Get and plot the results
counts = result.get_counts()
print("\nResult of the double-slit experiment: ", counts)

    Explanation:
        The circuit uses two qubits with Hadamard gates (qc.h(0) and qc.h(1)) to put them in superposition.
        The CNOT gate creates entanglement between the qubits.
        The resulting output is a distribution showing the interference pattern created by quantum superposition and entanglement.

4. Entanglement: Quantum Teleportation

Entanglement is the phenomenon where qubits become correlated such that their states are dependent on each other, no matter the distance between them. Here, we'll create a basic entanglement experiment.

from qiskit import QuantumCircuit, Aer, execute

# Create a quantum circuit with 2 qubits
qc = QuantumCircuit(2)

# Create entanglement between qubits using a Hadamard gate and CNOT gate
qc.h(0)
qc.cx(0, 1)

# Add measurement to both qubits
qc.measure_all()

# Execute the circuit on the simulator
simulator = Aer.get_backend('qasm_simulator')
result = execute(qc, simulator, shots=1024).result()

# Get and print the results
counts = result.get_counts()
print("\nResult of the entanglement experiment: ", counts)

    Explanation:
        The Hadamard gate (qc.h(0)) creates a superposition on qubit 0.
        The CNOT gate (qc.cx(0, 1)) entangles qubits 0 and 1.
        The result of the circuit shows entangled states where the measurement of one qubit instantly influences the state of the other qubit.

5. Visualizing Results

The output of these circuits will show the result in terms of counts of each measurement outcome. To visualize the result more clearly, you can use Qiskit's plotting capabilities.

from qiskit.visualization import plot_histogram

# Plot the result
plot_histogram(counts)

This generates a histogram showing the measurement outcomes, which will help visualize the distribution of states in your quantum experiments.
6. Running on IBM Quantum Computers

After developing and testing the circuit on a simulator, you can run the quantum circuit on actual IBM quantum computers.

# Get the backend from IBM Q
provider = IBMQ.get_provider(hub='ibm-q', group='open', project='main')
backend = provider.get_backend('ibmq_16_melbourne')

# Execute the quantum circuit on the actual IBM quantum device
job = execute(qc, backend, shots=1024)

# Monitor the job status
job_monitor(job)

# Get the results
result = job.result()
counts = result.get_counts()

# Plot the result
plot_histogram(counts)

    Explanation:
        Replace 'ibmq_16_melbourne' with any available backend from your IBM Q Experience account.
        The execute function will run the job on the selected quantum computer, and the job_monitor will display the progress.

Conclusion

In this tutorial, we explored the IBM Q Experience and Qiskit to demonstrate key quantum computing concepts:

    Superposition: Where a qubit exists in multiple states at once.
    Double-Slit Experiment: Interference patterns due to quantum superposition and entanglement.
    Entanglement: Where qubits are correlated in such a way that the state of one qubit affects the other instantaneously.

You can extend this by running experiments on real quantum computers through IBM's cloud service or by exploring more advanced quantum algorithms like Quantum Teleportation, Quantum Fourier Transform, and Shor's Algorithm.
