import networkx as nx
import matplotlib.pyplot as plt
import random

# Function to generate the one-dimensional ring network with additional random links
def generate_ring_with_random_links(N, p):
    G = nx.Graph()
    # Add nodes
    G.add_nodes_from(range(1, N+1))
    # Add edges for the ring structure
    for i in range(1, N):
        G.add_edge(i, i+1)
    G.add_edge(N, 1)  # Connect the last node to the first node to complete the ring
    # Add random edges independently between each pair of nodes
    for i in range(1, N+1):
        for j in range(i+1, N+1):
            if random.random() < p:
                G.add_edge(i, j)
    return G

# Parameters
N = 6  # Number of nodes
p = 0.5  # Probability of adding random links

# Generate the network
G = generate_ring_with_random_links(N, p)

# Draw the graph
pos = nx.circular_layout(G)
nx.draw(G, pos, with_labels=True, node_size=500, node_color="skyblue", font_size=12, font_weight="bold", edge_color="gray")
plt.title("One-Dimensional Ring Network with Random Links")
plt.show()
