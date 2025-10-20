[深度优先搜索（DFS）与广度优先搜索（BFS）_深度优先搜索和广度优先搜索对比-CSDN博客](https://blog.csdn.net/Summer_night_star/article/details/123512204)

## DFS算法

```java
class DFSGraph {
    private int vertices;
    private int[][] adjacencyMatrix;

    // 构造函数，初始化图的顶点数量和邻接矩阵
    public DFSGraph(int vertices) {
        this.vertices = vertices;
        // 初始化邻接矩阵，全部元素初始化为 0，表示没有边
        adjacencyMatrix = new int[vertices][vertices];
    }

    // 添加边的方法
    public void addEdge(int source, int destination) {
        // 在邻接矩阵中标记从源节点到目标节点有边，值为 1
        adjacencyMatrix[source][destination] = 1;
        // 对于无向图，从目标节点到源节点也有边，所以反向也标记为 1
        adjacencyMatrix[destination][source] = 1; 
    }

    // DFS 辅助方法，进行递归遍历
    private void dfsUtil(int vertex, boolean[] visited) {
        // 标记当前顶点已访问
        visited[vertex] = true; 
        // 输出当前顶点
        System.out.print(vertex + " "); 

        // 遍历所有顶点
        for (int i = 0; i < vertices; i++) {
            // 如果当前顶点和顶点 i 之间有边且顶点 i 未被访问
            if (adjacencyMatrix[vertex][i] == 1 &&!visited[i]) { 
                // 对未访问的邻接顶点进行递归调用
                dfsUtil(i, visited); 
            }
        }
    }

    // DFS 的入口方法
    public void dfs(int startVertex) {
        // 初始化访问数组，标记所有顶点未访问
        boolean[] visited = new boolean[vertices]; 
        // 调用辅助方法开始 DFS 遍历
        dfsUtil(startVertex, visited); 
    }

    public static void main(String[] args) {
        DFSGraph graph = new DFSGraph(5);
        // 添加边
        graph.addEdge(0, 1);
        graph.addEdge(0, 2);
        graph.addEdge(1, 3);
        graph.addEdge(1, 4);
        graph.addEdge(2, 4);

        System.out.println("DFS 遍历结果:");
        // 从顶点 0 开始进行 DFS 遍历
        graph.dfs(0); 
    }
}
```

## BFS算法

```java
import java.util.LinkedList;
import java.util.Queue;

class BFSGraph {
    private int vertices;
    private int[][] adjacencyMatrix;

    // 构造函数，初始化图的顶点数量和邻接矩阵
    public BFSGraph(int vertices) {
        this.vertices = vertices;
        // 初始化邻接矩阵，全部元素初始化为 0，表示没有边
        adjacencyMatrix = new int[vertices][vertices];
    }

    // 添加边的方法
    public void addEdge(int source, int destination) {
        // 在邻接矩阵中标记从源节点到目标节点有边，值为 1
        adjacencyMatrix[source][destination] = 1;
        // 对于无向图，从目标节点到源节点也有边，所以反向也标记为 1
        adjacencyMatrix[destination][source] = 1; 
    }

    // BFS 方法
    public void bfs(int startVertex) {
        // 初始化访问数组，标记所有顶点未访问
        boolean[] visited = new boolean[vertices]; 
        // 使用队列存储待访问的顶点
        Queue<Integer> queue = new LinkedList<>(); 
        // 标记起始顶点已访问
        visited[startVertex] = true; 
        // 将起始顶点加入队列
        queue.add(startVertex); 

        while (!queue.isEmpty()) {
            // 从队列中取出一个顶点
            int currentVertex = queue.poll(); 
            // 输出当前顶点
            System.out.print(currentVertex + " "); 

            // 遍历所有顶点
            for (int i = 0; i < vertices; i++) {
                // 如果当前顶点和顶点 i 之间有边且顶点 i 未被访问
                if (adjacencyMatrix[currentVertex][i] == 1 &&!visited[i]) { 
                    // 标记顶点 i 已访问
                    visited[i] = true; 
                    // 将顶点 i 加入队列
                    queue.add(i); 
                }
            }
        }
    }

    public static void main(String[] args) {
        BFSGraph graph = new BFSGraph(5);
        // 添加边
        graph.addEdge(0, 1);
        graph.addEdge(0, 2);
        graph.addEdge(1, 3);
        graph.addEdge(1, 4);
        graph.addEdge(2, 4);

        System.out.println("BFS 遍历结果:");
        // 从顶点 0 开始进行 BFS 遍历
        graph.bfs(0); 
    }
}
```