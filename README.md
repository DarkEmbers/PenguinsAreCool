# Least Cost

```java
public Journey leastCost(String from, String to) throws FlyingPlannerException
```

Find the least cost path between two vertexes in a graph.

### How
you already set the weights of the graph to be the cost of the flight. So use `djikstra's` algorithm to find the least cost path (aka the shortest path).
>DijkstraShortestPath

After you get the path it will be of type GraphPath<WhateverYou, PutHere> so you will need to convert it to a Journey. This can be done by using the `Journey` constructor where your stops are your `vertexList` and your flights are your `edgeList`.
```java
new Journey(your vertex list, your flight list);
```

# Least Hop

```java
public Journey leastHop(String from, String to) throws FlyingPlannerException
```

Find the least hop (flight changes) between two vertecies in a graph.

### How
For this you have to make sure your graph is unweighted otherwise the weights of the edges will affect the shortest path. Use `djikstra's` algorithm to find the least cost path.
>Since your weights don't exist, the algorithm will give least hops

How can you make you graph unweighted you ask (I know you too well), just create a new `directedMultigraph` (note not weighted), and add all vertecies and edges to this using loops (yes LOOPS!).

After you get the path it will be of type GraphPath<WhateverYou, PutHere> so you will need to convert it to a Journey. This can be done by using the `Journey` constructor where your stops are your `vertexList` and your flights are your `edgeList`.
```java
new Journey(your vertex list, your flight list);
```

# Least Cost / Hop, Excluding

```java
public Journey leastCost(String from, String to, List<String> excluding)
```
```java
public Journey leastHop(String from, String to, List<String> excluding)
```

Find the least hop / cost between to veticies but exclude some verticies from the resulting journey.

```
God all mighty how would i ever do this you say? Worry not, for I have a solution.
```

### How (Least Cost)
Create a new graph. Which one? Directed Weighted Multigraph of course. Add all the vertecies and edges to this graph. But when you add the verticies, check if they are in the `excluding` list. If they are, don't add them. When you add the edges, check if the source or destination are in the `excluding` list. If they are, don't add them.

### How (Least Hop)
Create a new graph. Which one? Directed Multigraph of course. Add all the vertecies and edges to this graph. But when you add the verticies, check if they are in the `excluding` list. If they are, don't add them. When you add the edges, check if the source or destination are in the `excluding` list. If they are, don't add them.

>Use good ol' Dijkstra's algorithm to find the least cost / hop path.

After you get the path it will be of type GraphPath<WhateverYou, PutHere> so you will need to convert it to a Journey. This can be done by using the `Journey` constructor where your stops are your `vertexList` and your flights are your `edgeList`.
```java
new Journey(your vertex list, your flight list);
```

# Least Hop Meet Up

```java
public String leastHopMeetUp(String at1, String at2) throws FlyingPlannerException
```

Find the least hop meet up point between two people.

### How
You obviously have had the revalation that when you use Dijkstra's algorithm from a vertex to another, you're getting the shortest path. So you can use this to find the least hop meet up point. 

>Quite the tricky task you say? Worry not, for I have hatcheted a plan.

Why don't you have a variable that stores the airport with the least hop meetup. Obviously it will be set to `null` at first. Also have a variable that stores how many hops it takes to get to that airport from both `at1` and `at2`.

```java
Airport meetUp = null;
int meetUpHops = -1; // -1 is null
```

Now have a loop (crazy right!?) that goes the the verticies (aka vertexList) of the graph and checks how many hops it takes to get to that vertex from both `at1` + how many hops it takes to get to that vertex from `at2`.

You can either check the number of stops by using `djikstra's` algorithm or you can use the leastHop method you made and get the `size` of the stops (airports or whatever you called it) list from the Journey.

If current meetUp is null, then clearly this is the first vertex you're checking. So set `meetUp` to the current vertex and `meetUpHops` to the sum of the two.

Else the sum of these two is less than the current `meetUpHops` then set `meetUp` to the current vertex and `meetUpHops` to the sum of the two.

After the loop is done, return the code of the airport.