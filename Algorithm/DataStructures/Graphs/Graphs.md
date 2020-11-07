# Graphs

## WHAT ARE GRAPHS
A __graph data structure__ consists of a finite (and possibly mutable) set of vertices or nodes or points, together with a set of unordered pairs of these vertices for an undirected __graph__ or a set of ordered pairs for a directed __graph__.

### USES FOR GRAPHS
- Social Networks
- Location / Mapping
- Routing Algorithms
- Visual Hierarchy
- File System Optimizations
- EVERYWHERE!

### ESSENTIAL GRAPH TERMS
- __Vertex__ - a node
- __Edge__ - connection between nodes
- __Weighted/Unweighted__ - values assigned to distances between vertices
- __Directed/Undirected__ - directions assigned to distanced between vertices

## Adjacency List
- Can take up less space (in sparse graphs)
- Faster to iterate over all edges
- Can be slower to lookup specific edge

        VS

## Adjacency Matrix
- Takes up more space (in sparse graphs)
- Slower to iterate over all edges
- Faster to lookup specific edge


## GRAPH CLASS
```javascript
class Graph {
    constructor(){
        this.adjacencyList = {}
    }
}
```
