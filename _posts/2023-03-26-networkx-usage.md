## Using Networkx

[Doc](https://networkx.org/documentation/stable/reference/introduction.html)

### Initialize Graph
```
import networkx as nx
G = nx.DiGraph()
```

### Add nodes

* Subset denotes layer of nodes in multipartite graph
* You can find it using topological sort (networkx or your own algo)
```
G.add_node(s, subset=gen_labels[s])
```

### Add edges with weight and color
```
G.add_edge(from_node,to_node,color='b',weight=2)
```

## Draw graph
```
import matplotlib.pyplot as plt

# get position dictionary
# you can use other layouts
pos_dict = nx.multipartite_layout(G)

# make slight changes to make graph planar
pos_dict["nodename"] = [0, 0.3]

plt.figure(3,figsize=(30,15))
plt.title("Selling Sedans and Engines", fontsize=20)
edges = G.edges()

# Get colors and weights from edges we already added
colors = [G[u][v]['color'] for u,v in edges] 
weights = [G[u][v]['weight'] for u,v in edges]

nx.draw(G, pos=pos_dict, node_size=1600, font_size=15, with_labels=True, arrowsize=20,
node_shape='v', edge_color=colors, width=weights)
```


### Appendix - Finding topological order and use it in multipartite graph
Build a temporary graph just to find topological labels
```
def get_generation_labels(G_temp):
    gen_labels = {}
    temp = nx.topological_generations(G_temp)
    for i,generation in enumerate(temp):
        for stage in generation: 
            gen_labels[stage] = 100-i #to make graph go left to right.
    return gen_labels
```
Use the labels to build new graph
```
gen_labels = get_generation_labels(G_temp) #we will throw away G_temp
G = nx.DiGraph()
for s in nodes:
    G.add_node(s, subset=gen_labels[s]) #set suset on node to layer number
```

