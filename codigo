import heapq

# Grafo de Rumania con distancias entre ciudades
graph = {
    'Arad': [('Zerind', 75), ('Sibiu', 140), ('Timisoara', 118)],
    'Zerind': [('Arad', 75), ('Oradea', 71)],
    'Oradea': [('Zerind', 71), ('Sibiu', 151)],
    'Sibiu': [('Arad', 140), ('Oradea', 151), ('Fagaras', 99), ('Rimnicu Vilcea', 80)],
    'Fagaras': [('Sibiu', 99), ('Bucharest', 211)],
    'Timisoara': [('Arad', 118), ('Lugoj', 111)],
    'Lugoj': [('Timisoara', 111), ('Mehadia', 70)],
    'Mehadia': [('Lugoj', 70), ('Drobeta', 75)],
    'Drobeta': [('Mehadia', 75), ('Craiova', 120)],
    'Craiova': [('Drobeta', 120), ('Rimnicu Vilcea', 146), ('Pitesti', 138)],
    'Rimnicu Vilcea': [('Sibiu', 80), ('Craiova', 146), ('Pitesti', 97)],
    'Pitesti': [('Rimnicu Vilcea', 97), ('Craiova', 138), ('Bucharest', 101)],
    'Bucharest': [('Fagaras', 211), ('Pitesti', 101)]
}

# Heurísticas estimadas desde cada ciudad hacia Bucarest
heuristics = {
    'Arad': 366, 'Zerind': 374, 'Oradea': 380, 'Sibiu': 253, 'Fagaras': 176,
    'Timisoara': 329, 'Lugoj': 244, 'Mehadia': 241, 'Drobeta': 242, 'Craiova': 160,
    'Rimnicu Vilcea': 193, 'Pitesti': 100, 'Bucharest': 0
}

def busqueda_a_estrella(graph, heuristics, start, goal):
    # Cola de prioridad para la lista abierta
    open_list = [(0, start)]
    heapq.heapify(open_list)
    
    # Costos g (distancia acumulada desde el inicio)
    g_costs = {start: 0}
    
    # Diccionario para almacenar el camino recorrido
    came_from = {}

    # Bucle principal de búsqueda
    while open_list:
        _, current = heapq.heappop(open_list)

        # En caso de llegar al destino, se reconstruye el camino
        if current == goal:
            return reconstruct_path(came_from, current)
        
        # Explorar los vecinos de la ciudad actual
        for neighbor, cost in graph[current]:
            new_g_cost = g_costs[current] + cost
            # Solo se agrega si encontramos un camino mejor
            if new_g_cost < g_costs.get(neighbor, float('inf')):
                came_from[neighbor] = current
                g_costs[neighbor] = new_g_cost
                f_cost = new_g_cost + heuristics[neighbor]
                heapq.heappush(open_list, (f_cost, neighbor))
                
    # En caso de no encuentrar el destino
    return None

def reconstruct_path(came_from, current):
    # Construcción del camino desde el destino al origen
    path = [current]
    while current in came_from:
        current = came_from[current]
        path.append(current)
    return path[::-1]

# Ejecución de la búsqueda A* en el mapa de Rumania
start_city = 'Arad'
destination_city = 'Bucharest'
path = busqueda_a_estrella(graph, heuristics, start_city, destination_city)

# Resultado de la ruta óptima
if path:
    print("Ruta óptima de", start_city, "a", destination_city, ":", " -> ".join(path))
else:
    print("No se encontró una ruta desde", start_city, "a", destination_city)
