# Epidemiology_And_Disease_Spread
When a disease spreads in a population, it's crucial to understand how it moves from person to person(or Location to Location). This is where graph theory becomes useful.
Graph Basics:
Nodes: Represent individuals, locations, or entities.
Edges: Represent the connections between nodes (e.g., interactions between individuals/Locations).

Contact Network:
A graph can model the interactions in a population. For example, in Hyderabad, each person can be a node/Location can be a Node, and an edge can represent a close contact or interaction where disease transmission can occur. Identifying articulation points becomes essential for understanding critical locations or individuals that can significantly influence the spread of infections. The goal is to pinpoint locations or individuals whose removal(Lockdown) could lead to a more fragmented network, potentially slowing down the spread of the disease. 

Example: COVID-19 in Hyderabad

Step 1: Data Collection
Gather Data:
Collect data on individuals' movements(or Locations), interactions, and COVID-19 cases in Hyderabad.
Sources: Contact tracing apps, mobile phone data, health records, and social networks.
Build the Graph:
Create a graph where each node represents a person in Hyderabad.
Draw edges between nodes if there has been an interaction between those individuals.

Step 2: Identify Key Points
Central Nodes:
Identify individuals with the most connections (high degree). These are "super spreaders" who can infect many others.
Articulation Points:
These are critical nodes whose removal would significantly disrupt the graph. In epidemiology, these points can be key locations or individuals whose isolation would break the chain of transmission.

Step 3: Disease Control Strategy:

Simulate Spread:
Use the graph to simulate how COVID-19 spreads from person to person.
Apply epidemiological models like SIR (Susceptible, Infected, Recovered) to see how the disease propagates through the network.

Step 4: Intervene at Key Points:

Target Interventions:
Vaccination: Prioritize vaccination for central nodes (super spreaders) and individuals at articulation points to prevent the disease from spreading rapidly.
Testing and Quarantine: Increase testing and quarantine efforts for these key individuals or locations.
Monitor and Control:
Continuous monitoring of the network to identify new key nodes as the situation evolves.
Use real-time data to adjust strategies, such as imposing localized lockdowns or travel restrictions in specific neighborhoods of Hyderabad.

Example Scenario in Hyderabad

Building the Contact Network:
Suppose we collect data on individuals in Hyderabad. Person A interacts with Persons B, C, and D; Person B interacts with Persons A and E, and so on.
We build a graph where nodes are people and edges represent interactions. 

Identifying Super Spreaders and Articulation Points:
Through analysis, we find Person A has many connections (super spreader) and that removing Person C (an articulation point) would break the network into smaller parts, reducing the disease's spread potential.

Simulating and Intervening:
Simulate disease spread starting from an infected individual and observe how it moves through the network.
Prioritize vaccinating Person A and isolating Person C to significantly control the spread.
Implement testing and quarantine around the neighborhoods of Persons A and C.

Tools and Technologies
Graph Visualization Software: Tools that can help visualize and analyze the contact network.
Epidemiological Models: Use models like SIR or SEIR (Susceptible, Exposed, Infected, Recovered) to simulate and predict disease spread.
Data Sources: Leverage data from contact tracing apps, health databases, and mobility data.

Summary

1. Collect Data: Gather interaction and mobility data between Locations/Individuals.
2. Build Graph: Model the population/Locations as a graph.
3. Identify Key Points: Find super spreaders and articulation points.
4. Simulate Spread: Use epidemiological models to predict disease spread.
5. Intervene: Target vaccinations, testing, and quarantines at key points.
6. Monitor: Continuously monitor and adjust strategies based on real-time data.

Approximations:
Population Data for Ten Areas in Hyderabad

0. Banjara Hills: 45,000
1. Jubilee Hills: 40,000
2. Madhapur: 50,000
3. Kondapur: 55,000
4. Gachibowli: 60,000
5. Hitech City: 35,000
6. Begumpet: 70,000
7. Secunderabad: 65,000
8. Charminar: 80,000
9. Abids: 30,000

Connections (Edges) between Areas

Banjara Hills - Jubilee Hills
Banjara Hills - Madhapur
Jubilee Hills - Madhapur
Madhapur - Kondapur
Madhapur - Hitech City
Kondapur - Gachibowli
Gachibowli - Hitech City
Gachibowli - Begumpet
Begumpet - Secunderabad
Secunderabad - Charminar
Charminar - Abids
Abids - Banjara Hills

Identify Potential Super Spreaders:

To identify potential super spreaders, you can look at nodes (areas) with high population and high degree (number of connections). Here's how you might approach this in Java:
Track the population for each node.
Identify nodes with high population.
Identify nodes with high degree.
Prioritize nodes that meet both criteria for vaccination.

>>>>> Thought process behind finding Articulation Point:
When do we say a vertex is an Articulation Point ? 1. (Corner Node)When Par = -1 and "disconnected" child nodes are greater than 1 2. When par != -1, and there is only one way to to reach (u to v), if 'u' is a AP, the discovery time of u will always be less than lowest discovery of v and their fellow neighbours, because u always comes before v and its fellow neighbours. THIS IS THE CONCEPT, that all i.e dt[u]< low[v] and not a parent, then u is considered AP. We can say "u" is an AP even when dt[u]= low[v], why ? Let's say a Cycle is formed at AP, then if we perform DFS for this cycle, dt[u]= low[v], so if we remove "u" here, still the graph gets separated. So finally, when par!=-1, and if dt[u]<=low[v], that an articulation point.
Lets also understand what's the importance of child node, what actually is Child node? When we are accessing a neighbour from curr node, there are 3 possibilities, the neighbour could be parent of the curr node, second, the neighbour is already visited by someone (therefore called ancestor- Back edge), third, when the node is Unvisited, this is said to be a Child of curr node. If your neighbour is already visited then even if we remove curr, the graph is still not separated. So we have to find child which nodes are unvisited and are greater than 1. Visualize the graph to understand this condition. 
We need Two arrays- Discovery time and Lowest discovery time to update when neighbours got discovered. We must also track parent, visisted array. 
Lets understand Two conditions here, how do we update discovery time and lowest discovery time, second, when do we check the AP condition.
We sais we need to track parent, discovery time and lowest discovery time. Why do we need to track parent? by doing this we ensure that the AP condition correctly identifies true APs rather than mistakenly identifying the parent child as a AP, because parent distance obviously will be less than child and our condition also falls under this. 
Now, how do we implement the code, a) if the neigh is parent, we don't do anything, we just continue (because we cannot say if it is a AP or not) b)if neigh is visited already, then definitely this is not AP and most important, if it was already visited then that means, it was discovered earlier, so  we will have to update the Lowest discovery time - by checking lowest of curr and discovery of neigh c) if a node is not visited, we perform DFS, we go on updating the disc and low, once we go to the depth and all neighbours are transvered, while we are backtracking we update the Low discovery by checking low of curr and low of neighbour. HERE we check the AP condition  "if dt[u]<= low[v]".   
IMPORTANT: Why did we update the lowest discovery while backtracking when we performed DFS: SIMPLIFIED EXPLANATION: Let's think of it as updating your knowledge of the quickest possible travel routed: A. Direct routes(traversing)- Intially, you record your arrival times based on direct travel. B. Discovering Shortcuts(already oka visited dorkithe): As you visit other cities, you might discover that some cities could have been reached earlier through different routes. C. Updating Knowledge(updating low values): When returning from the visit(backtracking), you update the earliest possible arrival times for the cities visited, reflecting the quickest routes discovered.      
WHY did we use discovery time (disc) of the neighbour instead of its low value, when neighbour is already visited? Using discovery time of the neighbour when its already visited (back edge) helps in considering direct routes back to earlier visited cities. This ensures the most accurate reflection of possible shortcuts and helps in identifying critical connections. In contrast, for non-back edge connections. 
Simple put, track par, disc, low. If node is already vis, no bridge, if it not visited, perform DFS, update times, while backtracking update lowest of needed, check bridge condition.
