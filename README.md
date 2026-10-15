
SLE-4: Final Viva & Architecture Decision Record (ADR)

Course: 02AML204 – Introduction to Artificial Intelligence

PRN: 25UAM052 

Name: Maitryee Dilip Jadhav (Maitryee Jadhav) 

Division: A 

GitHub / Portfolio Link: https://github.com/maitryeejadhav20/main_profilingS (https://github.com/maitryeejadhav20) 


PART A: Architecture Decision Record (ADR)
•	Title: Use of A* Search with Manhattan Distance Heuristic over Uninformed Search (BFS) 

•	Status: Accepted[cite: 1]

•	Date: [Insert Date][cite: 1]

1. Context
While developing the Grid-Based Maze Solver & Pathfinding System, the application needed to efficiently compute optimal paths across an 800×800 grid matrix containing dynamic obstacle walls. Because grid-based pathfinding can suffer from state-space explosion, choosing the right traversal mechanism was critical to ensure low latency and minimal resource overhead. The system required a reliable algorithm capable of navigating complex user-defined maze configurations without excessive CPU bottlenecks. 


2. Decision
We decided to implement A Search utilizing the Manhattan distance heuristic* as the primary pathfinding algorithm within the Search Engine container, supported by a Priority Queue (Open List) and a Hash-Set (Closed List). 


3. Alternatives Considered
•	Alternative 1: Breadth-First Search (BFS) – An uninformed layer-order search strategy using a standard queue. 

•	Alternative 2: Depth-First Search (DFS) – An uninformed graph traversal strategy using a stack (rejected due to non-optimality and risk of infinite loops in open grids).

•	Alternative 3: Greedy Best-First Search – Uses only heuristic values without path cost ($g(n)$), leading to suboptimal paths.

4. Rationale / Justification
The selection of A* Search is strongly backed by both empirical profiling data from SLE-2 and modular architecture principles from SLE-3: 


•	Profiling Evidence (SLE-2): Benchmarking across 20 iterations on an 800×800 grid proved that BFS consumed an average of ~450 ms per run while expanding ~280,000 nodes, with get_neighbors() choking 58% of total CPU runtime due to blind expansion. In contrast, A* Search reduced average execution time to ~210 ms and compressed node expansion down to ~95,000 nodes. 

•	Architectural Synergy (SLE-3): By decoupling the Heuristic Module from the core Search Engine, A* cleanly computes $f(n) = g(n) + h(n)$ via Manhattan distance calculations. Furthermore, utilizing an explicit Explored Set (Closed List) mapped to a hash-set lookup structure guarantees $O(1)$ node checks, preventing redundant evaluations. 

5. Consequences
•	Positive:


o	Significantly faster execution speeds (~210 ms vs ~450 ms) and lower memory overhead. 

o	Highly targeted node exploration, cutting down unnecessary expansions by nearly 66%. 

•	Negative / Trade-offs:


o	Slightly higher implementation complexity due to priority queue management (heapq) and heuristic function overhead compared to standard queues. 

PART B: Short Summary of My SLE Journey
My software journey began in SLE-1 with the creation of the core agent search code, AI contribution tracking, and initial README setup[cite: 1]. In SLE-2, I benchmarked the system on an 800×800 grid using py-spy, proving quantitatively that A* outperforms BFS by reducing execution time from ~450 ms to ~210 ms. Moving into SLE-3, I structured the system into a modular C4 architecture—separating the Input Module, Search Engine, Heuristic Module, and Output Module—while defining precise data structures like Priority Queues and Closed Lists. Finally, in SLE-4, I consolidated these findings into this Architecture Decision Record (ADR) to formally justify why A* Search is the optimal choice for our pathfinding system. 


PART C: AI Contribution Note
•	AI tools used: Gemini / ChatGPT 

•	What AI helped with: Generating structural templates, assisting with C4 diagram syntax formatting, and providing command-line guidance for running py-spy profiling metrics. 

•	What I did myself: Configured the custom Python codebase, executed benchmark tests across 20 iterations, analyzed flame graphs, mapped out modular component interactions, and wrote the final analytical justifications. 

PART D: Viva Preparation Notes (Quick Key Points)
1.	Core Decision: Chose A* Search with Manhattan distance over BFS because informed search directs traversal toward the goal, avoiding blind expansion. 

2.	Profiling Proof (SLE-2): A* ran in ~210 ms (expanding ~95,000 nodes) compared to BFS at ~450 ms (expanding ~280,000 nodes). 

3.	Architecture (SLE-3): The decoupled Heuristic Module feeds h(n) into the Search Engine's priority queue, while the closed hash-set ensures O(1) lookup times. 

4.	C4 Container Overview: User inputs configuration - Input Module parses data - Search Engine executes A* using the Heuristic Module -Output Module renders final metrics. 


Conclusion:
Completing SLE-4 serves as the culmination of the entire pathfinding system design journey. By evaluating empirical performance metrics and modular C4 diagrams, selecting A Search with Manhattan Distance* was proven to be the most optimal architectural choice for balancing computational speed, memory efficiency, and search precision. Progressing systematically through code implementation (SLE-1), py-spy profiling (SLE-2), C4 architectural design (SLE-3), and this formal ADR justification (SLE-4) successfully bridges theoretical AI concepts with practical software engineering. Furthermore, utilizing AI tools responsibly for formatting and structure while maintaining complete student ownership over all empirical data and code guarantees a thoroughly defended, production-ready system. 

