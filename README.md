vector<int> shortestPath(int N,int E, vector<vector<int>>& edges)
{
    vector<pair<int, int>> adj[N];
    for(int i=0; i<E; i++)
    {
         int u = edges[i][0];
         int v = edges[i][1];
         int wt = edges[i][2];          
         adj[u].push_back({v,wt});
    }
    vector<int> dist(N, INT_MAX);
    queue<pair<int, int>> q;
    q.push({0,0});
    dist[0]=0;
    while(!q.empty())
    {
        auto temp = q.front();
        q.pop();
        int curr_node = temp.first;
        for(auto adj_node : adj[curr_node])
        {
            int next_node = adj_node.first;
            int edge_weight = adj_node.second;
            if(dist[next_node] > dist[curr_node] + edge_weight)
            {
                dist[next_node] = dist[curr_node] + edge_weight;
                q.push({next_node , dist[next_node]});
            }
        }
    }
    for(int i=0; i<N; i++)
        if(dist[i]==INT_MAX) 
            dist[i]=-1;
    return dist;
}
