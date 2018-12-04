
## BFS, DFS
Breadth-first and depth-first search are two exhaustive search algorithms. BFS is guaranteed to find the optimal solution, while DFS often finds a (possibly sub-optimal) solution faster.

## Tree search vs Graph Search, Uniform Cost Search
Graph search and tree search can both be used to explore the same spaces. The primary difference is that graph search does NOT expand a single node more than once, while binary search may return to the same node and expand it multiple times. Both Tree Search and Graph Search are variations of Uniform Cost Search.

### Dijkstra's Algorithm
A variant of Uniform Cost Search that finds the shortest path between all nodes on a weighted di-graph.

## A* Search
A* search is a type of informed search and is useful for searching a weighted graph. A* Search makes use of both the cost of the path to the current location and a heuristic function to estimate the value of each state (i.e. its proximity to the goal) to make its search decisions.

### Admissible & Consistent Heuristics

**Admissible**: A heuristic h is admissible if 0 <= h(n) <= h*(n) for all states n, where h*(n) is the true cost of reaching the goal from state n.

**Consistent**: A heuristic is consistent if h(n) – h(m) ≤ h\*(n to m) for all states n and m for which there is a path from n to m. All consistent heuristics are also admissible.

## Minimax
The minimax algorithm is an adversarial search technique that applies when one agent (MAX) wants to maximize a score and the other(s) (MIN) wants to minimize it. It assumes the opponent, MIN, behaves optimally. The algorithm looks ahead to the opponent's next move (or next n moves) and makes the optimal decision based on the opponent's expected behavior.

### alpha-beta pruning
Alpha-beta pruning is an adaptation to minimax that "prunes" branches from the ssearch tree based on stored alpha and beta values representing maximum and minumum values along a branch.

## Expectimax
Expectimax modifies the minimax problem to account for opponents who behave unpredictably. Decisions are based on the expected value of branches rather than their minumum or maximum. Both minimax and expectimax often use evaluation functions to estimate the value of non-terminal states in search trees of non-trivial size. Good expectimax performance depends on some knowledge of the probability of the opponent making a given decision.

## Markov Decision Processes
A Markov model is made up of a set of states, actions, a transition function, rewards, and start/terminal states. The outcome of each action (s') depends only on the current state. An MDP search tree resembles an Expectimax search tree. The goal with a MDP is to produce an optimal policy, which maps all states to their optimal actions based on expected reward.

### Bellman Updates
The Bellman update starts with the current set of values (V, Q, Pi) over a given domain. An iterative update is made to each value, propagating the maximum expected value (based on the current set of values). In all the Iteration algorithms below, a discount is applied to future rewards when calculating expected value to account for uncertain outcomes (i.e. a reward now is better than a reward later).

**Value Iteration**: Value iteration applies the Bellman update to V(s)->(Real Number), the expected value of each state.

**Q-value Iteration**: Q-value Iteration applies the Bellman update to the maximum expected value of each state/action pair, Q(s,a)->(Real Number).

**Policy Iteration**: Policy Iteration applies the Bellman update to the policy Pi(s)->a. Instead of the maximum expected value, the update supplies the argmax of the expected value, or the action that produces the maximum expected value.

## Reinforcement Learning

### Model-based vs Model-Free

**Model-based Reinforcement Learning** treats the task at hand like a Markov Decsion Process where the trasition probabilities (T) and rewards (R) are unknown. The agent takes actions and attempts to "fill in" T and R. It can then extract an "optimal" policy using an iterative techique like the ones above.

**Model-Free Reinforcement Learning** stores pertinent information (e.g. about state and expected payouts) and takes action based on these without attempting to create a model of the entire environment.

### Direct Evaluation
The actor keeps track of a policy and the average (discounted) reward resulting from visiting that state, V(s). At the end of each episode, average rewards are updated. Direct evaluation does not provide a mechanism for leveraging information about connections between states.

### Temporal Difference Learning
Instead of updating at the end of each episode, the vaue of each state V(s) is updated after each transition. TD Learning solves the problem of extracting information from the relationships between states because the most likely successor state s' will more frequently affect the update of state s.

### Q-learning

Q-learning is an online learning algorithm, meaning the agent does not make "trial runs" to collect information before acting, but rather collects information as it acts. Instead of tracking the value V of each state, Q-learning tracks Q(s,a) of state-action pairs. After each action a from state s, Q(s,a) is updated with the new reward information. Changes to Q(s,a) are weighted by a learning rate alpha. Q-learning converges to an optimal policy, even if the agent is acting suboptimally.

**Epsilon-greedy**: In order to efficiently explore the entire state space, a tradeoff between exploiting known advantageous paths and exploring unknown paths must be made. Epsilon-greedy is a Q-learning serch strategy in which the agent acts randomly with a small probability epsilon, and otherwise acts optimally according to the Q-values it has learned so far. In order to avoid random thrashing after convergence, epsilon can be decreased over time.
