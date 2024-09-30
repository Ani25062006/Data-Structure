# Data-Structure
import tkinter as tk
from tkinter import scrolledtext
from collections import defaultdict
import heapq
import itertools

# ADT class implementation
class ADT:
    def __init__(self):
        self.data = []

    def insert(self, value):
        self.data.append(value)

    def delete(self):
        if self.data:
            return self.data.pop(0)
        return None

    def traverse(self):
        return self.data

# Stack class implementation
class Stack:
    def __init__(self):
        self.stack = []

    def push(self, value):
        self.stack.append(value)

    def pop(self):
        if self.stack:
            return self.stack.pop()
        return None

    def traverse(self):
        return self.stack

# Singly Linked List implementation
class Node:
    def __init__(self, value):
        self.value = value
        self.next = None

class SinglyLinkedList:
    def __init__(self):
        self.head = None

    def insert(self, value):
        new_node = Node(value)
        if not self.head:
            self.head = new_node
        else:
            current = self.head
            while current.next:
                current = current.next
            current.next = new_node

    def traverse(self):
        current = self.head
        elements = []
        while current:
            elements.append(current.value)
            current = current.next
        return elements

# Doubly Linked List implementation
class DNode:
    def __init__(self, value):
        self.value = value
        self.next = None
        self.prev = None

class DoublyLinkedList:
    def __init__(self):
        self.head = None

    def insert(self, value):
        new_node = DNode(value)
        if not self.head:
            self.head = new_node
        else:
            current = self.head
            while current.next:
                current = current.next
            current.next = new_node
            new_node.prev = current

    def traverse(self):
        current = self.head
        elements = []
        while current:
            elements.append(current.value)
            current = current.next
        return elements

# Queue implementation
class Queue:
    def __init__(self):
        self.queue = []

    def enqueue(self, value):
        self.queue.append(value)

    def dequeue(self):
        if self.queue:
            return self.queue.pop(0)
        return None

    def traverse(self):
        return self.queue

# Priority Queue implementation
class PriorityQueue:
    def __init__(self):
        self.pq = []

    def insert(self, value):
        heapq.heappush(self.pq, value)

    def delete(self):
        if self.pq:
            return heapq.heappop(self.pq)
        return None

    def traverse(self):
        return self.pq

# Binary Tree implementation
class TreeNode:
    def __init__(self, value):
        self.value = value
        self.left = None
        self.right = None

class BinaryTree:
    def __init__(self):
        self.root = None

    def insert(self, value):
        if not self.root:
            self.root = TreeNode(value)
        else:
            self._insert(self.root, value)

    def _insert(self, node, value):
        if value < node.value:
            if node.left is None:
                node.left = TreeNode(value)
            else:
                self._insert(node.left, value)
        else:
            if node.right is None:
                node.right = TreeNode(value)
            else:
                self._insert(node.right, value)

    def inorder_traversal(self, node, result):
        if node:
            self.inorder_traversal(node.left, result)
            result.append(node.value)
            self.inorder_traversal(node.right, result)
        return result

# Graph implementation
class Graph:
    def __init__(self):
        self.graph = defaultdict(list)

    def add_edge(self, u, v):
        self.graph[u].append(v)

    def bfs(self, start):
        visited = []
        queue = [start]
        while queue:
            node = queue.pop(0)
            if node not in visited:
                visited.append(node)
                queue.extend(self.graph[node])
        return visited

    def dfs(self, start, visited=None):
        if visited is None:
            visited = []
        visited.append(start)
        for neighbor in self.graph[start]:
            if neighbor not in visited:
                self.dfs(neighbor, visited)
        return visited

# Traveling Salesman Problem (TSP) using brute force
def traveling_salesman_problem(graph, start):
    n = len(graph)
    all_points = list(range(n))
    shortest_path = float('inf')
    best_route = None
    
    for perm in itertools.permutations(all_points):
        if perm[0] == start:
            current_length = sum(graph[perm[i]][perm[i+1]] for i in range(n-1)) + graph[perm[-1]][start]
            if current_length < shortest_path:
                shortest_path = current_length
                best_route = perm
    return best_route, shortest_path

# Basic Hash Table implementation
class HashTable:
    def __init__(self):
        self.table = [None] * 10  # Size of 10 for simplicity

    def insert(self, key, value):
        index = key % len(self.table)
        self.table[index] = value

    def delete(self, key):
        index = key % len(self.table)
        self.table[index] = None

    def traverse(self):
        return [(index, value) for index, value in enumerate(self.table) if value is not None]

# Hash Table with Collision Handling (Overflow Chaining)
class HashTableWithCollision:
    def __init__(self):
        self.table = [[] for _ in range(10)]  # Size of 10

    def insert(self, key, value):
        index = key % len(self.table)
        self.table[index].append(value)

    def delete(self, key, value):
        index = key % len(self.table)
        if value in self.table[index]:
            self.table[index].remove(value)

    def traverse(self):
        return [(index, values) for index, values in enumerate(self.table) if values]

# Main Application with Data Structures Button
class DataStructureApp:
    def __init__(self, root):
        self.root = root
        self.root.title("Data Structures GUI Ananya yadav")
        self.root.geometry("600x400")
        self.root.configure(bg="gray")  # Set background color to gray

        # College title in bold
        title_label = tk.Label(self.root, text="SHETH L.U.J.& SIR M.V. COLLEGE OF ARTS, SCIENCE", 
                               font=("Arial", 14, "bold"), bg="gray")
        title_label.pack(pady=10)
        title_label = tk.Label(self.root, text="Ananya yadav S122", 
                               font=("Arial", 10, "bold"), bg="gray")
        title_label.pack(pady=5)

        # Create Data Structures button
        ds_button = tk.Button(self.root, text="Data Structures", font=("Arial", 12), bg="green", fg="white", 
                              command=self.open_data_structure_window)
        ds_button.pack(pady=20)

    def open_data_structure_window(self):
        # Create a new window for Data Structures
        ds_window = tk.Toplevel(self.root)
        ds_window.title("Data Structures Ananya yadav")
        ds_window.geometry("400x600")
        ds_window.configure(bg="lightgray")

        # Buttons for different data structures
        buttons = [
            ("ADT", self.adt_window),
            ("Stack", self.stack_window),
            ("Singly Linked List", self.sll_window),
            ("Doubly Linked List", self.dll_window),
            ("Queue", self.queue_window),
            ("Priority Queue", self.pq_window),
            ("Binary Tree", self.binary_tree_window),
            ("Graph", self.graph_window),
            ("Breadth First Tree", self.breadth_first_tree_window),
            ("Depth First Tree", self.depth_first_tree_window),
            ("Traveling Salesman Problem", self.tsp_window),
            ("Basic Hash Table", self.basic_hash_table_window),
            ("Hash Table with Collision Handling", self.hash_table_with_collision_window)
        ]

        for text, command in buttons:
            button = tk.Button(ds_window, text=text, command=command, width=25, height=2, font=("Arial", 12))
            button.pack(pady=10)

    def create_code_window(self, title, code, output):
        code_window = tk.Toplevel(self.root)
        code_window.title(title)
        code_window.geometry("400x400")

        label_code = tk.Label(code_window, text="Code:", font=("Arial", 12))
        label_code.pack(pady=5)

        code_text = scrolledtext.ScrolledText(code_window, wrap=tk.WORD, width=50, height=10)
        code_text.pack(pady=5)
        code_text.insert(tk.END, code)
        code_text.config(state=tk.DISABLED)

        label_output = tk.Label(code_window, text="Output:", font=("Arial", 12))
        label_output.pack(pady=5)

        output_text = scrolledtext.ScrolledText(code_window, wrap=tk.WORD, width=50, height=10)
        output_text.pack(pady=5)
        output_text.insert(tk.END, output)
        output_text.config(state=tk.DISABLED)

    # Individual windows for each data structure
    def adt_window(self):
        adt = ADT()
        adt.insert(1)
        adt.insert(2)
        output = f"ADT Traversal: {adt.traverse()}"
        code = """class ADT:
    def __init__(self):
        self.data = []

    def insert(self, value):
        self.data.append(value)

    def delete(self):
        if self.data:
            return self.data.pop(0)
        return None

    def traverse(self):
        return self.data"""
        self.create_code_window("ADT", code, output)

    def stack_window(self):
        stack = Stack()
        stack.push(1)
        stack.push(2)
        output = f"Stack Traversal: {stack.traverse()}"
        code = """class Stack:
    def __init__(self):
        self.stack = []

    def push(self, value):
        self.stack.append(value)

    def pop(self):
        if self.stack:
            return self.stack.pop()
        return None

    def traverse(self):
        return self.stack"""
        self.create_code_window("Stack", code, output)

    def sll_window(self):
        sll = SinglyLinkedList()
        sll.insert(1)
        sll.insert(2)
        output = f"Singly Linked List Traversal: {sll.traverse()}"
        code = """class Node:
    def __init__(self, value):
        self.value = value
        self.next = None

class SinglyLinkedList:
    def __init__(self):
        self.head = None

    def insert(self, value):
        new_node = Node(value)
        if not self.head:
            self.head = new_node
        else:
            current = self.head
            while current.next:
                current = current.next
            current.next = new_node

    def traverse(self):
        current = self.head
        elements = []
        while current:
            elements.append(current.value)
            current = current.next
        return elements"""
        self.create_code_window("Singly Linked List", code, output)

    def dll_window(self):
        dll = DoublyLinkedList()
        dll.insert(1)
        dll.insert(2)
        output = f"Doubly Linked List Traversal: {dll.traverse()}"
        code = """class DNode:
    def __init__(self, value):
        self.value = value
        self.next = None
        self.prev = None

class DoublyLinkedList:
    def __init__(self):
        self.head = None

    def insert(self, value):
        new_node = DNode(value)
        if not self.head:
            self.head = new_node
        else:
            current = self.head
            while current.next:
                current = current.next
            current.next = new_node
            new_node.prev = current

    def traverse(self):
        current = self.head
        elements = []
        while current:
            elements.append(current.value)
            current = current.next
        return elements"""
        self.create_code_window("Doubly Linked List", code, output)

    def queue_window(self):
        queue = Queue()
        queue.enqueue(1)
        queue.enqueue(2)
        output = f"Queue Traversal: {queue.traverse()}"
        code = """class Queue:
    def __init__(self):
        self.queue = []

    def enqueue(self, value):
        self.queue.append(value)

    def dequeue(self):
        if self.queue:
            return self.queue.pop(0)
        return None

    def traverse(self):
        return self.queue"""
        self.create_code_window("Queue", code, output)

    def pq_window(self):
        pq = PriorityQueue()
        pq.insert(1)
        pq.insert(2)
        output = f"Priority Queue Traversal: {pq.traverse()}"
        code = """class PriorityQueue:
    def __init__(self):
        self.pq = []

    def insert(self, value):
        heapq.heappush(self.pq, value)

    def delete(self):
        if self.pq:
            return heapq.heappop(self.pq)
        return None

    def traverse(self):
        return self.pq"""
        self.create_code_window("Priority Queue", code, output)

    def binary_tree_window(self):
        bt = BinaryTree()
        bt.insert(2)
        bt.insert(1)
        bt.insert(3)
        output = f"Binary Tree Inorder Traversal: {bt.inorder_traversal(bt.root, [])}"
        code = """class TreeNode:
    def __init__(self, value):
        self.value = value
        self.left = None
        self.right = None

class BinaryTree:
    def __init__(self):
        self.root = None

    def insert(self, value):
        if not self.root:
            self.root = TreeNode(value)
        else:
            self._insert(self.root, value)

    def _insert(self, node, value):
        if value < node.value:
            if node.left is None:
                node.left = TreeNode(value)
            else:
                self._insert(node.left, value)
        else:
            if node.right is None:
                node.right = TreeNode(value)
            else:
                self._insert(node.right, value)

    def inorder_traversal(self, node, result):
        if node:
            self.inorder_traversal(node.left, result)
            result.append(node.value)
            self.inorder_traversal(node.right, result)
        return result"""
        self.create_code_window("Binary Tree", code, output)

    def graph_window(self):
        g = Graph()
        g.add_edge(0, 1)
        g.add_edge(0, 2)
        g.add_edge(1, 3)
        output = f"BFS: {g.bfs(0)}\nDFS: {g.dfs(0)}"
        code = """class Graph:
    def __init__(self):
        self.graph = defaultdict(list)

    def add_edge(self, u, v):
        self.graph[u].append(v)

    def bfs(self, start):
        visited = []
        queue = [start]
        while queue:
            node = queue.pop(0)
            if node not in visited:
                visited.append(node)
                queue.extend(self.graph[node])
        return visited

    def dfs(self, start, visited=None):
        if visited is None:
            visited = []
        visited.append(start)
        for neighbor in self.graph[start]:
            if neighbor not in visited:
                self.dfs(neighbor, visited)
        return visited"""
        self.create_code_window("Graph", code, output)

    def breadth_first_tree_window(self):
        # This is a placeholder for BFS Tree implementation
        output = "This is a placeholder for Breadth First Tree implementation."
        code = """def breadth_first_tree():
    pass  # Implement BFS Tree logic here"""
        self.create_code_window("Breadth First Tree", code, output)

    def depth_first_tree_window(self):
        # This is a placeholder for DFS Tree implementation
        output = "This is a placeholder for Depth First Tree implementation."
        code = """def depth_first_tree():
    pass  # Implement DFS Tree logic here"""
        self.create_code_window("Depth First Tree", code, output)

    def tsp_window(self):
        graph = [[0, 10, 15, 20],
                 [10, 0, 35, 25],
                 [15, 35, 0, 30],
                 [20, 25, 30, 0]]
        start = 0
        route, distance = traveling_salesman_problem(graph, start)
        output = f"Best Route: {route}\nShortest Distance: {distance}"
        code = """def traveling_salesman_problem(graph, start):
    # Implement TSP logic here
    pass"""
        self.create_code_window("Traveling Salesman Problem", code, output)

    def basic_hash_table_window(self):
        ht = HashTable()
        ht.insert(1, "A")
        ht.insert(2, "B")
        output = f"Hash Table: {ht.traverse()}"
        code = """class HashTable:
    def __init__(self):
        self.table = [None] * 10  # Size of 10 for simplicity

    def insert(self, key, value):
        index = key % len(self.table)
        self.table[index] = value

    def delete(self, key):
        index = key % len(self.table)
        self.table[index] = None

    def traverse(self):
        return [(index, value) for index, value in enumerate(self.table) if value is not None]"""
        self.create_code_window("Basic Hash Table", code, output)

    def hash_table_with_collision_window(self):
        ht = HashTableWithCollision()
        ht.insert(1, "A")
        ht.insert(11, "B")  # Collision
        output = f"Hash Table with Collision Handling: {ht.traverse()}"
        code = """class HashTableWithCollision:
    def __init__(self):
        self.table = [[] for _ in range(10)]  # Size of 10

    def insert(self, key, value):
        index = key % len(self.table)
        self.table[index].append(value)

    def delete(self, key, value):
        index = key % len(self.table)
        if value in self.table[index]:
            self.table[index].remove(value)

    def traverse(self):
        return [(index, values) for index, values in enumerate(self.table) if values]"""
        self.create_code_window("Hash Table with Collision Handling", code, output)

# Main program
if __name__ == "__main__":
    root = tk.Tk()
    app = DataStructureApp(root)
    root.mainloop()
