LA1) def selection_sort(arr):
      n = len(arr)
    sorted_arr = arr.copy()
    for i in range(n):
        min_idx = i
        for j in range(i + 1, n):
            if sorted_arr[j] < sorted_arr[min_idx]:
                min_idx = j
        sorted_arr[i], sorted_arr[min_idx] = sorted_arr[min_idx], sorted_arr[i]   
    return sorted_arr
def bubble_sort(arr):
    n = len(arr)
    sorted_arr = arr.copy()
     for i in range(n):
        swapped = False
        for j in range(0, n - i - 1):
            if sorted_arr[j] > sorted_arr[j + 1]:
                sorted_arr[j], sorted_arr[j + 1] = sorted_arr[j + 1], sorted_arr[j]
                swapped = True
        if not swapped:
            break        
    return sorted_arr
def display_top_five(sorted_arr):
    print("\nx--- Top Scores ---x")
    n = len(sorted_arr)
      if n == 0:
        print("No student records available.")
       print("--------------x----------------")
        return
top_scores = sorted_arr[-1:-6:-1]
     for rank, score in enumerate(top_scores, start=1):
print(f"Rank {rank}: {score:.2f}%")
        print("--------------x----------------")
def main():
    percentages = []
    count = int(input("Enter the number of students: "))
    print("--------------x----------------")
    for i in range(count):
        score = float(input(f"Enter percentage for student {i + 1}: "))
        percentages.append(score)
 print("-------------------------------")
    print("\nOriginal Percentages:", percentages)
    selection_sorted = selection_sort(percentages)
    print("--------------x----------------")
    print("\nSorted using Selection Sort (Ascending):", selection_sorted)
    bubble_sorted = bubble_sort(percentages)
    print("--------------x----------------")
    print("Sorted using Bubble Sort (Ascending):", bubble_sorted)
    print("--------------x----------------")
    display_top_five(bubble_sorted)
if __name__ == "__main__":
    main()

    
LA 4)def traverse(arr):
    if not arr:
        print("Array is empty.")
    else:
        print(f"Current Array: {arr}")
        print("-------------x---------------")
def insert_element(arr, element, index):
    if index < 0 or index > len(arr):
        print("Error: Invalid index position.")
        print("-------------x---------------")
    else:
        arr.insert(index, element)
        print(f"Successfully inserted {element} at index {index}.")
        print("-------------x---------------")
def delete_element(arr, index):
    if not arr:
        print("Error: Array is empty (Underflow).")
        print("-------------x---------------")
    elif index < 0 or index >= len(arr):
        print("Error: Invalid index position.")
        print("-------------x---------------")
    else:
        removed = arr.pop(index)
        print(f"Successfully deleted {removed} from index {index}.")
        print("-------------x---------------")
def linear_search(arr, target):
    for i in range(len(arr)):
        if arr[i] == target:
            return i
    return -1
def main():
    arr = []
        while True:
        try:
            n = int(input("Enter the initial size of the array: "))
  if n < 0:
                print("Size cannot be negative. Try again.")
                print("-------------x---------------")
                continue
            break
        except ValueError:
            print("Error: Please enter a valid integer size.")
            print("-------------x---------------")
    if n > 0:
        print(f"Enter {n} space-separated integers for the array:")
        while True:
            try:
                elements = list(map(int, input().split()))
                if len(elements) != n:
                    print(f"Error: Expected {n} elements, but got {len(elements)}. Please try again:")
                    continue
                arr = elements
                break
            except ValueError:
                print("Error: Invalid input. Please enter integers only:")
                print("-------------x---------------")
 print("\nInitial array created successfully!")
    traverse(arr)
    while True:
        print("\nx--- 1D ARRAY OPERATIONS MENU ---x")
        print("1. Insertion")
        print("2. Deletion")
        print("3. Traversal")
        print("4. Linear Search")
        print("5. Exit")
        print("------------x---------------")
        choice = input("Enter your choice (1-5): ")
        print("-------------x---------------")
        if choice == '1':
            try:
                val = int(input("Enter value to insert: "))
                print("-------------x---------------")
                idx = int(input(f"Enter index (0 to {len(arr)}): "))
                insert_element(arr, val, idx)
            except ValueError:
                print("Error: Please enter valid integers.")
                print("-------------x---------------")
       
        elif choice == '2':
            try:
                idx = int(input("Enter index to delete: "))
                print("-------------x---------------")
                delete_element(arr, idx)
            except ValueError:
                print("Error: Please enter a valid integer index.")
                print("-------------x---------------")
        elif choice == '3':
            traverse(arr)
        elif choice == '4':
            try:               
target = int(input("Enter value to search: "))
                result = linear_search(arr, target)
                if result != -1:
                    print(f"Element {target} found at index {result}.")
                    print("-------------x---------------")
                else:
                    print(f"Element {target} not found in the array.")
                    print("-------------x---------------")
            except ValueError:
    
            print("Error: Please enter a valid integer value.")
                print("-------------x---------------")
        elif choice == '5':
            print("Exiting program.")
            print("x-------------x---------------x")
            break
        else:
            print("Invalid choice! Please select an option from 1 to 5.")
            print("-------------x---------------")
if __name__ == "__main__":
main()


LA 5)class Node:
    def __init__(self, name, time):
        self.name = name
        self.time = time       # Stored as minutes for easy sorting
        self.prev = None
        self.next = None
class AppointmentList:
    def __init__(self):
        self.head = None
        self.tail = None 
# Convert minutes into 12-hour format
    def format_time(self, minutes):
        hour = minutes // 60
      
  minute = minutes % 60
        period = "AM" if hour < 12 else "PM"
        display_hour = hour % 12
        if display_hour == 0:
            display_hour = 12
        return f"{display_hour:02d}:{minute:02d} {period}"
    # Convert user input into minutes
    def convert_to_minutes(self, time):
        try:
            time_part, period = time.strip().upper().split()
            hour, minute = map(int, time_part.split(":"))
            if period not in ["AM", "PM"]:
                return None
            if hour < 1 or hour > 12 or minute < 0 or minute > 59:
                return None
            # Convert to 24-hour internally
            if period == "AM":
                if hour == 12:
                    hour = 0
            else:
                if hour != 12:
                    hour += 12


            total_minutes = hour * 60 + minute
            # Appointment allowed from 9:00 AM to 4:00 PM
            if total_minutes < 9 * 60 or total_minutes > 16 * 60:
                return None
            # Only full-hour appointments
            if minute != 0:
                return None
            return total_minutes
        except ValueError:
            return None
    # Check if time is already booked
    def search_time(self, time):
        current = self.head
        while current:
            if current.time == time:
                return True
            current = current.next
        return False
    # Display free slots
    def display_free_slots(self):
        print("\nAvailable Time Slots:")


    for hour in range(9, 17):
            time = hour * 60
            if not self.search_time(time)            
  print(self.format_time(time))
    # Book appointment
    def book_appointment(self):
        name = input("Enter patient name: ")
        time_input = input("Enter appointment time (e.g., 10:00 AM): ")
        time = self.convert_to_minutes(time_input)
        if time is None:
            print("Invalid time!")
            print("Please enter a time between 09:00 AM and 04:00 PM.")
            return
        if self.search_time(time):
            print("This time slot is already booked!")
            return
        new_node = Node(name, time)  
 if self.head is None:
            self.head = self.tail = new_node
       

 else:
            new_node.prev = self.tail
            self.tail.next = new_node
            self.tail = new_node
        print("Appointment booked successfully.")
        print("Time:", self.format_time(time))
    # Sort using pointer manipulation
    def sort_by_time(self):
        if self.head is None or self.head.next is None:
            print("List is already sorted.")
            return
        current = self.head.next
        while current:
            next_node = current.next
            previous = current.prev     
  # Find correct position
            while previous and previous.time > current.time:
                previous = previous.prev
            # Remove current node
            if current.prev:
                current.prev.next = current.next


            if current.next:
                current.next.prev = current.prev
            else:
                self.tail = current.prev
            # Insert at beginning
            if previous is None:
                current.prev = None
                current.next = self.head
                self.head.prev = current
                self.head = current
            # Insert after previous    
else:                
current.next = previous.next
                current.prev = previous
                if previous.next:
                    previous.next.prev = current
                else:
                    self.tail = current
                previous.next = current
            current = next_node
    print("Appointments sorted by time.")

    # Display appointments
    def display_appointments(self):
        if self.head is None:
            print("\nNo appointments booked.")
            return
  print("\nBooked Appointments:")
        current = self.head
        while current:
            print(f"{self.format_time(current.time)} - {current.name}")
            current = current.next
    # Cancel appointment
    def cancel_appointment(self):
        time_input = input("Enter appointment time to cancel (e.g., 02:00 PM): ")
        time = self.convert_to_minutes(time_input)
        if time is None:
            print("Invalid time!")
            return
        current = self.head
        while current:
            if current.time == time:
                # Update previous node
             
   if current.prev:
                    current.prev.next = current.next
                else:
                    self.head = current.next
                # Update next node
                if current.next:
                    current.next.prev = current.prev
                else:
                    self.tail = current.prev
                print("Appointment cancelled successfully.")
                return
            current = current.next
        print("No appointment found at", self.format_time(time))
# Main program
appointments = AppointmentList()
while True:
    print("\n========== APPOINTMENT SYSTEM ==========")
    print("1. Display Free Slots")
    print("2. Book Appointment")
    print("3. Display Appointments")
    print("4. Sort Appointments by Time")
  

  print("5. Cancel Appointment")
    print("6. Exit")
    choice = input("Enter your choice: ")
    if choice == "1":
        appointments.display_free_slots()
    elif choice == "2":
        appointments.book_appointment()
    elif choice == "3":
        appointments.display_appointments()
    elif choice == "4":
        appointments.sort_by_time()
    elif choice == "5":
        appointments.cancel_appointment()
    elif choice == "6":
        print("Program terminated.")
        break
    else:
        print("Invalid choice!")


LA 6)class Node:
    """Represents an individual node in the linked list."""
    def __init__(self, data):
        self.data = data
        self.next = None
class LinkedListStack:
    """Stack implementation using a singly linked list."""
    def __init__(self):
        self.top = None
        self._size = 0
    def push(self, data):
"""Insert an element at the top of the stack (head of linked list)."""
        new_node = Node(data)
        new_node.next = self.top
        self.top = new_node
       
 self._size += 1
    def pop(self):
        """Remove and return the top element."""
        if self.is_empty():
            raise IndexError("pop from an empty stack")
        popped_value = self.top.data
        self.top = self.top.next
        self._size -= 1
        return popped_value
    def peek(self):
        """Return the top element without removing it."""
        if self.is_empty():
            raise IndexError("peek from an empty stack")
        return self.top.data
    def is_empty(self)
 """Check whether the stack is empty."""
        return self.top is None
    def __len__(self):
        return self._size
def apply_operator(op1, op2, operator):
    """Apply the binary operator to operands."""
    if operator == '+':
        
return op1 + op2
    elif operator == '-':
        return op1 - op2
    elif operator == '*':
        return op1 * op2
    elif operator == '/':
        if op2 == 0:
            raise ZeroDivisionError("Division by zero")
        return op1 / op2
    elif operator in ('^', '**'):
        return op1 ** op2
  else:
        raise ValueError(f"Unsupported operator: {operator}")
def evaluate_postfix(expression: str) -> float:  
  """
    Evaluates a postfix expression string where tokens are separated by spaces.
    Supports integers, floats, and operators (+, -, *, /, ^).
    """
    stack = LinkedListStack()
    tokens = expression.strip().split()
    operators = {'+', '-', '*', '/', '^', '**'}
  
  
for token in tokens:
        if token not in operators:
            # Parse token as number (float or int)
            try:
                num = float(token)
                stack.push(num)
            except ValueError:
                raise ValueError(f"Invalid token encountered: '{token}'")
        else:
            # An operator requires two operands
 if len(stack) < 2:
                raise ValueError("Malformed postfix expression: insufficient operands.")
            op2 = stack.pop()  # First pop is the right operand
            op1 = stack.pop()  # Second pop is the left operand
            result = apply_operator(op1, op2, token)          
  stack.push(result)
    if len(stack) != 1:
        raise ValueError("Malformed postfix expression: too many operands remaining.")
    return stack.pop()
if __name__ == "__main__":
    test_cases = [
        "2 3 1 * + 9 -",          # (2 + (3 * 1)) - 9 = -4.0
     
   "100 200 + 2 / 5 * 7 +",  # ((100 + 200) / 2) * 5 + 7 = 757.0
        "2 3 ^ 4.5 +",            # (2^3) + 4.5 = 12.5
        "15 7 1 1 + - / 3 * 2 1 1 + + -"  # Complex multi-operator expression
    ]
    for expr in test_cases:
        res = evaluate_postfix(expr)
        print(f"Postfix : {expr}") 
print(f"Result  : {res}\n")


LA 7)class DequeArray:
    """Deque mapped to a 1D fixed-size list using circular index arithmetic."""
    def __init__(self, capacity: int):
        self.capacity = capacity
        self.arr = [None] * capacity
        self.front = -1
        self.rear = -1
        self.size = 0
    def is_full(self) -> bool:
        return self.size == self.capacity
    def is_empty(self) -> bool:
        return self.size == 0

    def insert_front(self, val):
        if self.is_full():
            print(f"Overflow: Cannot insert {val} at front.")
            return
        if self.is_empty():
            self.front = 0
            self.rear = 0
        else:
            self.front = (self.front - 1 + self.capacity) % self.capacity
        self.arr[self.front] = val
        self.size += 1
    def insert_rear(self, val):
        if self.is_full():
            print(f"Overflow: Cannot insert {val} at rear.")
            return
        if self.is_empty():
            self.front = 0
            self.rear = 0
        else:
            self.rear = (self.rear + 1) % self.capacity
        self.arr[self.rear] = val
        self.size += 1


    def delete_front(self):
        if self.is_empty():
            print("Underflow: Deque is empty.")
            return None
        val = self.arr[self.front]
        self.arr[self.front] = None
        if self.front == self.rear:
            self.front = -1
            self.rear = -1
        else:
            self.front = (self.front + 1) % self.capacity
        self.size -= 1
        return val
    def delete_rear(self):
        if self.is_empty():
            print("Underflow: Deque is empty.")
            return None
        val = self.arr[self.rear]
        self.arr[self.rear] = None
        if self.front == self.rear:
            self.front = -1
  
          self.rear = -1
        else:
            self.rear = (self.rear - 1 + self.capacity) % self.capacity
        self.size -= 1
        return val
    def display(self):
        if self.is_empty():
            print("Deque is empty.")
            return
        elements = []
        idx = self.front
        for _ in range(self.size):
            elements.append(str(self.arr[idx]))
            idx = (idx + 1) % self.capacity
        print("Deque (Front -> Rear): " + " -> ".join(elements))
if __name__ == "__main__":
    dq = DequeArray(5)
    dq.insert_rear(10)
    dq.insert_rear(20)
    dq.insert_front(5)
    dq.insert_rear(30)
    dq.insert_front(1)

    dq.display()
    dq.delete_front()
    dq.delete_rear()
    dq.display()
    dq.insert_front(99)
    dq.insert_rear(88)
dq.display()


AI 1) from collections import deque
def bfs(graph, start_node):
    visited = set()
    queue = deque([start_node])
    visited.add(start_node)
    bfs_order = []
    while queue:
        current_node = queue.popleft()
        bfs_order.append(current_node)
        for neighbor in graph[current_node]:
            if neighbor not in visited:
                visited.add(neighbor)
           
     queue.append(neighbor)
    return bfs_order
if __name__ == "__main__":
    graph = {
        'A': ['B', 'C'],
        'B': ['A', 'D', 'E'],
        'C': ['A', 'F'],
        'D': ['B'],
        'E': ['B', 'F'],
        'F': ['C', 'E']
    }
    print("BFS Traversal starting from node 'A':")
    result = bfs(graph, 'A')
print(" -> ".join(result))


AI 2)def dfs_recursive(graph, node, visited=None):
   if visited is None:
        visited = set()
    visited.add(node)
    print(node, end=" ")
    for neighbor in graph.get(node, []):
        if neighbor not in visited:
            dfs_recursive(graph, neighbor, visited)
def dfs_iterative(graph, start_node)
    visited = set()
    stack = [start_node]
    while stack:
     node = stack.pop()

        if node not in visited:
            print(node, end=" ")
            visited.add(node)
            for neighbor in reversed(graph.get(node, [])):
                if neighbor not in visited:
                    stack.append(neighbor)
if __name__ == "__main__":  
    graph = {
        'A': ['B', 'C'],
        'B': ['D', 'E'],
        'C': ['F'],
        'D': [],
        'E': ['F'],
        'F': []
    }
    print("DFS Traversal (Recursive starting from vertex A):")
    dfs_recursive(graph, 'A')
    print("\nx----------x----------x")

   
 print("\n\nDFS Traversal (Iterative starting from vertex A):")
    dfs_iterative(graph, 'A')
    print("\nx----------x----------x")



AI 3)import tkinter as tk
from tkinter import messagebox
root = tk.Tk()
root.title("Tic Tac Toe")
current_player = "X"
buttons = []
def check_winner():
    # Winning combinations
    win_positions = [
        (0, 1, 2), (3, 4, 5), (6, 7, 8),  # Rows
        (0, 3, 6), (1, 4, 7), (2, 5, 8),  # Columns
        (0, 4, 8), (2, 4, 6)               # Diagonals
    ]
    for a, b, c in win_positions:
        if buttons[a]["text"] == buttons[b]["text"] == buttons[c]["text"] != "":
            return True

    return False
def button_click(index):
    global current_player
    if buttons[index]["text"] == "":
        buttons[index]["text"] = current_player
        if check_winner():
            messagebox.showinfo("Winner", current_player + " Wins!")
            reset_game()
        elif all(button["text"] != "" for button in buttons):
            messagebox.showinfo("Result", "Match Draw!")
            reset_game()

        else:
            if current_player == "X":
                current_player = "O"
            else:
                current_player = "X"

def reset_game():
    global current_player

    for button in buttons:
        button["text"] = ""

    current_player = "X"

# Create 9 buttons
for i in range(9):
    button = tk.Button(
        root,
        text="",
        font=("Arial", 20),
        width=5,
        height=2,
        command=lambda i=i: button_click(i)
    )
    button.grid(row=i // 3, column=i % 3)
    buttons.append(button)
root.mainloop()


AI 4)import tkinter as tk
from tkinter import messagebox

root = tk.Tk()
root.title("8 Puzzle")
root.geometry("350x400")

# Initial puzzle
puzzle = [1, 2, 3,
          4, 0, 6,
          7, 5, 8]

# Goal state
goal = [1, 2, 3,
        4, 5, 6,
        7, 8, 0]
buttons = []
def display():
    for i in range(9):
        if puzzle[i] == 0:
            buttons[i].config(text="")
        else:
            buttons[i].config(text=str(puzzle[i]))

def move(index):
    zero = puzzle.index(0)

    # Check if clicked tile is next to blank space
    possible_moves = []

    row = zero // 3
    col = zero % 3

    if row > 0:
        possible_moves.append(zero - 3)   # Up

    if row < 2:
        possible_moves.append(zero + 3)   # Down

    if col > 0:
        possible_moves.append(zero - 1)   # Left

    if col < 2:
        possible_moves.append(zero + 1)   # Right

    if index in possible_moves:
        puzzle[zero], puzzle[index] = puzzle[index], puzzle[zero]

        display()

        if puzzle == goal:
            messagebox.showinfo("Congratulations", "Puzzle Solved!")


def reset():
    global puzzle

    puzzle = [1, 2, 3,
              4, 0, 6,
              7, 5, 8]

    display()


# Create 9 buttons
for i in range(9):

    btn = tk.Button(
        root,
        text="",
        font=("Arial", 22, "bold"),
        width=5,
        height=2,
        command=lambda i=i: move(i)
    )

    btn.grid(row=i // 3, column=i % 3, padx=3, pady=3)

    buttons.append(btn)


# Reset button
reset_button = tk.Button(
    root,
    text="Reset",
    font=("Arial", 14),
    command=reset
)

reset_button.grid(row=3, column=0, columnspan=3, pady=15)

display()

root.mainloop()


AI 5)import tkinter as tk
from tkinter import messagebox
from collections import deque

# Jug capacities
JUG1 = 4
JUG2 = 3
TARGET = 2


# BFS function
def solve_bfs():

    # Initial state
    start = (0, 0)

    # Queue for BFS
    queue = deque([start])

    # Visited states
    visited = {start}

    # Store parent of each state
    parent = {start: None}

    while queue:

        current = queue.popleft()
        a, b = current

        # Goal check
        if a == TARGET or b == TARGET:

            path = []

            while current is not None:
                path.append(current)
                current = parent[current]

            path.reverse()

            show_solution(path)
            return

        # Possible operations

        states = [

            # Fill Jug 1
            (JUG1, b),

            # Fill Jug 2
            (a, JUG2),

            # Empty Jug 1
            (0, b),

            # Empty Jug 2
            (a, 0),

            # Pour Jug 1 -> Jug 2
            (
                a - min(a, JUG2 - b),
                b + min(a, JUG2 - b)
            ),

            # Pour Jug 2 -> Jug 1
            (
                a + min(b, JUG1 - a),
                b - min(b, JUG1 - a)
            )
        ]

        # Add new states to queue
        for state in states:

            if state not in visited:

                visited.add(state)
                queue.append(state)
                parent[state] = current

    messagebox.showinfo("Result", "No solution exists!")


# Display solution
def show_solution(path):

    solution_text.delete("1.0", tk.END)

    solution_text.insert(
        tk.END,
        "BFS SOLUTION\n"
        "============\n\n"
    )

    for i, state in enumerate(path):

        solution_text.insert(
            tk.END,
            f"Step {i}: Jug 1 = {state[0]} L, "
            f"Jug 2 = {state[1]} L\n"
        )

    solution_text.insert(
        tk.END,
        "\n🎉 Goal Reached: 2 Litres!"
    )


# ---------------- GUI ----------------

root = tk.Tk()

root.title("Water Jug Problem - BFS")
root.geometry("600x500")


# Title
title = tk.Label(
    root,
    text="💧 WATER JUG PROBLEM",
    font=("Arial", 22, "bold")
)

title.pack(pady=15)


# Problem information
info = tk.Label(
    root,
    text="Jug 1 = 4 Litres    |    Jug 2 = 3 Litres\n"
         "Goal = Measure exactly 2 Litres",
    font=("Arial", 14)
)

info.pack(pady=10)


# BFS button
solve_button = tk.Button(
    root,
    text="🤖 SOLVE USING BFS",
    font=("Arial", 14, "bold"),
    width=25,
    command=solve_bfs
)

solve_button.pack(pady=20)


# Solution display
solution_text = tk.Text(
    root,
    width=55,
    height=15,
    font=("Courier New", 12)
)

solution_text.pack(pady=10)


# Start GUI
root.mainloop()
