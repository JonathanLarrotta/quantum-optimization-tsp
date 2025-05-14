# 🚀 Optimización Cuántica vs. Clásica en TSP/Logística  
*"Comparando Hopfield, grafos y métodos cuánticos (QAOA/Annealing) para problemas de rutas"*  

---

## 🔍 **Problema: TSP y Logística**  
**Definición clásica**:  
- Encontrar la ruta más corta que visita **N ciudades** una vez y regresa al origen (complejidad O(n!)).  

**Aplicación logística**:  
- Minimizar costos y tiempos en distribución (ej: última milla).  

---

## ⚖️ **Comparativa: Métodos Clásicos vs. Cuánticos**  

### 1. **Enfoque Clásico**  
#### a) Redes de Hopfield (como en tu repositorio)  
```python

pip install qiskit dwave-ocean-sdk networkx
git clone https://github.com/tu-usuario/quantum-tsp-logistics.git

# Ejemplo simplificado (Tour no válido vs. válido)
import numpy as np

# Matriz de distancias (ejemplo para 4 ciudades)
distancias = np.array([
    [0, 2, 9, 10],
    [2, 0, 6, 4],
    [9, 6, 0, 8],
    [10, 4, 8, 0]
])

# Función de energía para Hopfield
def energia(estado, distancias):
    return np.sum(estado * distancias @ estado.T)

# Solución con grafos (ejemplo usando NetworkX)
import networkx as nx

G = nx.Graph()
G.add_weighted_edges_from([(0,1,2), (0,2,9), (1,2,6), (1,3,4), (2,3,8)])
ruta_optima = nx.approximation.traveling_salesman_problem(G, cycle=True)

# Ejemplo para TSP en D-Wave (usando dwave-ocean-sdk)
from dwave.system import DWaveSampler

# Definir QUBO para TSP (matriz de acoplamientos)
qubo = {(0,1): -2, (0,2): -9, (1,2): -6, ...}  # Pesos negativos para minimización

# Ejecutar en computador cuántico
response = DWaveSampler().sample_qubo(qubo, num_reads=1000)
print("Mejor ruta:", response.first.sample)

# Implementación QAOA para TSP
from qiskit.algorithms import QAOA
from qiskit_optimization import QuadraticProgram

qp = QuadraticProgram()
qp.binary_var('x01')  # Ruta ciudad 0 -> 1
qp.minimize(linear={'x01': 2, 'x02': 9, ...})  # Minimizar distancia total

qaoa = QAOA(reps=3, quantum_instance=backend_simulator)
result = qaoa.compute_minimum_eigenvalue(qp.to_ising()[0])

# Usar QAOA con datos reales (matriz de distancias desde API)
distancias = obtener_distancias_api(lugares=["Cra 80 #20", "Cl 10 #45", ...])
qp = QuadraticProgram()
# ... (definir problema)
resultado = QAOA().solve(qp)
visualizar_ruta(resultado)
