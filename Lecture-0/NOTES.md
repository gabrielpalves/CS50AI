# Lecture 0

# SEARCH

	When a computer tries to search for a solution to a problem.

> ### Agent
> Entity that perceives its environment and acts upon that environment, e.g. a representation of a car that is trying to figure out how to arrive at a destination, in a problem of driving directions.

> ### State
> A configuration of the agent in its environment. Initial state is where the agent begin, i.e. the starting point of our algorithm.

> ### Actions
> Choices that can be made in a state. `ACTION(s)` returns the set of actions that can be made in state `s`.

> ### Transition model
> A description of the result `RESULT(s,a)` we get after we perform some available action `a` in state `s`.

> ### State space
> The set of all states we can get from the initial state by any sequence of actions.

> ### Goal test
> Some way to determine wheter a state is a goal state.

> ### Path cost
> Numerical cost associated with a given path. The optimal solution has the lowest path cost.

> ### Node
> A data structure to keep track of a variety of different values.
> - a state
> - a parent (node that generated this node)
> - an action (action applied to parent to get node)
> - a path cost (from initial state to node)

---


## Uninformed search
	Search strategy that uses no problem-specific knowledge, e.g. DFS and BFS.

> ### Depth-First Search (DFS)
> - Start with a frontier that contains the initial state. The frontier will return a solution or it will be empty (no solution found).
> - Start with an empty explored set.
> - Repeat:
> 	+ If the frontier is empty, there is nothing left to explore.
> 	+ Remove a node from the frontier.
> 	+ If node contains goal state, return the solution.
> 	+ Add the node to the explored set.
> 	+ Expand node, add resulting node to the frontier if they aren't already in the explored set. We can use stack to determine the next node to explore.
> 	
> > #### Stack
> > In the frontier: Last-in, first-out.

> ### Breadth-First Search (BFS)
> Explore the shallowest node in the frontier (queue) instead of the deepest (stack).
> 
> > #### Queue
> > First-in, first-out data type.

> ### DFS vs BFS
> DFS might explore less in some cases, meaning less memory usage, but BFS might be faster to find a solution in certain cases. When a solution is close to the beginning, but there are other way more expensive paths, then BFS would probably be better, because you can get unlucky in DFS because it can choose randomly a path that is actually very deep and expensive.

---


## Informed search
	Search strategy that uses problem-specific knowledge to find solutions more efficiently.
> 
> ### Greedy best-first search (GBFS)
> Expands the node that is closest to the goal, as estimated by a heuristic function `h(n)`.

> ### A* search
> Expands node with lowest `g(n) + h(n)` value.
> - g(n) = cost to reach node
> - h(n) = estimated cost to goal
> Optimal if:
> - h(n) is admissible (never overestimates the true cost), and
> - h(n) is consistent (for every node `n` and successor `n'` with step cost `c`, `h(n) < h(n') + c`)

---


# Game

> - `S0`: initial state
> - `Player(s)`: returns which player to move in state `s`
> - `Action(s)`: returns legal moves in state `s`
> - `Result(s,a)`: returns state after action `a` taken in state `s`
> - `Terminal(s)`: checks if state `s` is a terminal state
> - `Utility(s)`: final numerical value for terminal state `s`

> ## Minimax
> - Given a state `s`
> 	+ `MAX` picks action `a` in `Action(s)` that produces highest value of `Min-Value(Result(s,a))`
> 	+ `MIN` picks action `a` in `Action(s)` that produces smallest value of `Max-Value(Result(s,a))`
> 
> > ### Alpha-Beta Pruning
> > Optimization for the `Minimax` algorithm where I don't need to search through everything.
> > 
> > If I want to maximize a min value and I know that one of the possibilities of an action is smaller than all the possibilities of another action, then I don't need to calculate the value of the other possibilities for that action.