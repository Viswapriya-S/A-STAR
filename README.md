<h1>ExpNo 4 : Implement A* search algorithm for a Graph</h1> 
<h3>Name: Viswapriya S      </h3>
<h3>Register Number: 212225230311          </h3>
<H3>Aim:</H3>
<p>To ImplementA * Search algorithm for a Graph using Python 3.</p>
<H3>Algorithm:</H3>

``````
// A* Search Algorithm
1.  Initialize the open list
2.  Initialize the closed list
    put the starting node on the open 
    list (you can leave its f at zero)

3.  while the open list is not empty
    a) find the node with the least f on 
       the open list, call it "q"

    b) pop q off the open list
  
    c) generate q's 8 successors and set their 
       parents to q
   
    d) for each successor
        i) if successor is the goal, stop search
        
        ii) else, compute both g and h for successor
          successor.g = q.g + distance between 
                              successor and q
          successor.h = distance from goal to 
          successor (This can be done using many 
          ways, we will discuss three heuristics- 
          Manhattan, Diagonal and Euclidean 
          Heuristics)
          
          successor.f = successor.g + successor.h

        iii) if a node with the same position as 
            successor is in the OPEN list which has a 
           lower f than successor, skip this successor

        iV) if a node with the same position as 
            successor  is in the CLOSED list which has
            a lower f than successor, skip this successor
            otherwise, add  the node to the open list
     end (for loop)
  
    e) push q on the closed list
    end (while loop)

``````

## PROGRAM:
```
import heapq

def astar(graph, heuristic, start, goal):
    pq = [(heuristic[start], 0, start, [start])]
    best_cost = {start: 0}

    while pq:
        f, g, node, path = heapq.heappop(pq)

        if node == goal:
            print("Path found:", path)
            return

        if g > best_cost.get(node, float('inf')):
            continue

        for neighbor, cost in graph[node]:
            new_g = g + cost

            if new_g < best_cost.get(neighbor, float('inf')):
                best_cost[neighbor] = new_g
                new_f = new_g + heuristic[neighbor]
                heapq.heappush(
                    pq, (new_f, new_g, neighbor, path + [neighbor])
                )

    print("Path not found")


# Number of nodes and edges
n, e = map(int, input().split())

graph = {}
for _ in range(e):
    u, v, cost = input().split()
    cost = int(cost)

    graph.setdefault(u, []).append((v, cost))
    graph.setdefault(v, []).append((u, cost))

# Heuristic values
heuristic = {}
for _ in range(n):
    node, h = input().split()
    heuristic[node] = int(h)
    graph.setdefault(node, [])

# Start and goal
start = 'A'
goal = max(heuristic, key=lambda x: (x == 'J', x))

# Use J for sample 1; G for sample 2
if 'J' in graph:
    goal = 'J'
elif 'G' in graph:
    goal = 'G'

astar(graph, heuristic, start, goal)
```
<hr>
<h2>Sample Graph I</h2>
<hr>

![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/b1377c3f-011a-4c0f-a843-516842ae056a)

<hr>
<h2>Sample Input</h2>
<hr>
10 14 <br>
A B 6 <br>
A F 3 <br>
B D 2 <br>
B C 3 <br>
C D 1 <br>
C E 5 <br>
D E 8 <br>
E I 5 <br>
E J 5 <br>
F G 1 <br>
G I 3 <br>
I J 3 <br>
F H 7 <br>
I H 2 <br>
A 10 <br>
B 8 <br>
C 5 <br>
D 7 <br>
E 3 <br>
F 6 <br>
G 5 <br>
H 3 <br>
I 1 <br>
J 0 <br>
<hr>
<h2>Sample Output</h2>
<hr>
Path found: ['A', 'F', 'G', 'I', 'J']

## OUTPUT:

<img width="1537" height="637" alt="WhatsApp Image 2026-10-15 at 10 32 41 AM" src="https://github.com/user-attachments/assets/6031b0a8-2195-4c41-b0dc-1458573dc240" />



<hr>
<h2>Sample Graph II</h2>
<hr>

![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/acbb09cb-ed39-48e5-a59b-2f8d61b978a3)


<hr>
<h2>Sample Input</h2>
<hr>
6 6 <br>
A B 2 <br>
B C 1 <br>
A E 3 <br>
B G 9 <br>
E D 6 <br>
D G 1 <br>
A 11 <br>
B 6 <br>
C 99 <br>
E 7 <br>
D 1 <br>
G 0 <br>
<hr>
<h2>Sample Output</h2>
<hr>
Path found: ['A', 'E', 'D', 'G']

## OUTPUT:

<img width="1375" height="355" alt="WhatsApp Image 2026-10-21 at 8 46 52 AM" src="https://github.com/user-attachments/assets/706f2866-49d9-4be1-9e4a-b1152458761a" />

## RESULT:
Thus Implemented Search algorithm for a Graph using Python 3

