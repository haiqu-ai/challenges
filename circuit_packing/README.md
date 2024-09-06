QPU Circuit Packing
Summary
This research project explores efficient methods for packing small quantum circuits onto larger quantum processing units (QPUs). The objective is to develop packing algorithms that significantly reduce the number of required shots, while accepting a controlled reduction in the fidelity of the results.

Background
Quantum circuits currently running on QPUs typically fall into two categories: they either use many qubits and have shallow depth, or they use very few qubits but are relatively deep. This is largely due to the high noise levels in Noisy Intermediate-Scale Quantum (NISQ) devices. For instance, when running a 20-qubit circuit on IBM's 127-qubit Eagle processor, the circuit is transpiled to run on 20 of the available qubits, leaving 107 qubits unused.

Challenge Objective
The challenge is to devise an algorithm that replicates a user's quantum circuit multiple times, packing these copies into a larger circuit that runs on a single QPU. The algorithm should reduce the number of shots in proportion to the number of copies packed. After execution, the results from the individual copies must be merged to restore the original shot count requested by the user. The key challenge lies in placing these copies in such a way that the reduction in fidelity is minimized.

Several factors contribute to performance degradation, including:

Qubit Placement
On a QPU, certain qubits perform better than others. The layout transpilation stage in Qiskit selects the optimal qubits for a given circuit to ensure the best possible results. Utilizing previously unused qubits is likely to result in lower performance, although typically, the performance does not degrade drastically as more qubits are employed.

For example, consider the error per layered gate from the IBM Fez device:

___image___

The challenge is to select qubits for the replicated circuits in a way that maximizes performance. A greedy approach could be used, where the best available qubits are selected for each additional copy.

Crosstalk
One source of coherent noise arises from unwanted resonances during the application of radio-frequency (RF) pulses to implement quantum gates on neighboring qubits. This phenomenon, known as crosstalk, can degrade the performance of circuits placed too close to one another. Further discussion of this issue can be found in the paper, QuCloud+: A Holistic Qubit Mapping Scheme for Single/Multi-programming on 2D/3D NISQ Quantum Computers.

Thus, an important consideration in packing the circuit copies is the proximity of the circuits to each other.

Submission Format
Participants are required to submit the following:

A tutorial/notebook demonstrating the proposed packing approach and the corresponding reduction in shot count.
A tradeoff analysis discussing the fidelity of the results compared to the shot savings achieved.