# ExpNo:10 Implementation of Classical Planning Algorithm

<h3>Name: SUJITHA ESTHER S       </h3>
<h3>Register Number: 212224060266 </h3>
<H3> Algorithm or Steps Involved:</H3>
<ol>
  <li>Define the initial state</li>
  <li>Define the goal state</li>
  <li>Define the actions</li>
  <li>Find a <b>plan</b> to reach the goal state</li>
  <li>Print the plan</li>
</ol>

# Example - 1
```
initial_state = {'A': 'Table', 'B': 'Table'}
goal_state = {'A': 'B', 'B': 'Table'}

actions = {
    'move_A_to_B': {'precondition': {'A': 'Table', 'B': 'Table'}, 'effect': {'A': 'B'}},
    'move_B_to_Table': {'precondition': {'A': 'Table', 'B': 'B'}, 'effect': {'B': 'Table'}}
}

plan = find_plan(initial_state, goal_state, actions)
print(plan)
```
# Output:
```
['move_A_to_B']
```
# Example - 2
```
initial_state = {'A': 'Table', 'B': 'Table', 'C': 'Table'}
goal_state = {'A': 'B', 'B': 'C', 'C': 'Table'}

actions = {
    'move_A_to_B': {'precondition': {'A': 'Table', 'B': 'Table'}, 'effect': {'A': 'B'}},
    'move_B_to_C': {'precondition': {'A': 'B', 'B': 'Table', 'C': 'Table'}, 'effect': {'B': 'C'}},
    'move_C_to_Table': {'precondition': {'A': 'B', 'B': 'C', 'C': 'C'}, 'effect': {'C': 'Table'}}
}

plan = find_plan(initial_state, goal_state, actions)
print(plan)
```
# Output:
```
['move_A_to_B', 'move_B_to_C']
```

<h3>PROGRAM</h3>
```python
    
    # Program: BFS-based Planner
    class Action:
        def __init__(self, name, effect):
            self.name = name
            self.effect = effect  # function(state) -> new_state
            
        def apply(self, state):
        return self.effect(state)
        
    def find_plan(initial_state, goal_state, actions):
         
        from collections import deque

        # Queue for BFS: stores tuples (current_state, plan_so_far)
        frontier = deque([(initial_state, [])])
        visited = set()

        while frontier:
            state, plan = frontier.popleft()
       
            if state == goal_state:
                return plan  

            # Avoid revisiting states
            if state in visited:
                continue
            visited.add(state)

            # Try all possible actions
            for action in actions:
                new_state = action.apply(state)  # action should define 'apply'
                if new_state not in visited:
                    frontier.append((new_state, plan + [action.name]))

        return None  # No plan found
    # Example usage
    move_left = Action("move_left", lambda s: s - 1)
    move_right = Action("move_right", lambda s: s + 1)
    actions = [move_left, move_right]

    initial_state = 0
    goal_state = 3

    plan = find_plan(initial_state, goal_state, actions)
    print("Plan:", plan)



<h3>OUTPUT</h3>
<img width="546" height="127" alt="Screenshot 2025-10-10 155131" src="https://github.com/user-attachments/assets/7551a621-6347-4b33-9986-0bb57ae00ebb" />

