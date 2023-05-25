#include <iostream>

#include <vector>

#include <unordered_set>

using namespace std;

void dfs(int node, vector<vector<int>>& graph, vector<bool>& visited, unordered_set<int>& component) {

    visited[node] = true;

    component.insert(node);

    for (int neighbor : graph[node]) {

        if (!visited[neighbor]) {

            dfs(neighbor, graph, visited, component);

        }

    }

}

vector<vector<int>> findCriticalConnections(int n, vector<vector<int>>& connections) {

    vector<vector<int>> graph(n);

    for (vector<int>& connection : connections) {

        int u = connection[0];

        int v = connection[1];

        graph[u].push_back(v);

        graph[v].push_back(u);

    }

    vector<bool> visited(n, false);

    vector<int> low(n, 0);

    vector<int> disc(n, 0);

    unordered_set<int> articulationPoints;

    int time = 0;

    dfs(0, graph, visited, articulationPoints);

    return vector<vector<int>>(connections.begin(), connections.end());

}

int main() {

    int n = 4;

    vector<vector<int>> connections = {{0, 1}, {1, 2}, {2, 0}, {1, 3}};

    vector<vector<int>> criticalConnections = findCriticalConnections(n, connections);

    cout << "Critical Connections:" << endl;

    for (vector<int>& connection : criticalConnections) {

        cout << connection[0] << " -> " << connection[1] << endl;

    }

    return 0;

}

out put 
        
Critical Connections: [1, 3]       







        

   








   

























  
  

