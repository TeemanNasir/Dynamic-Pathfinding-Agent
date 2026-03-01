# Dynamic-Pathfinding-Agent
This project implements a Dynamic Pathfinding Agent using informed search algorithms. The agent navigates a grid while adapting to dynamic obstacles using real-time re-planning.
Features

Interactive grid-based environment

Algorithms:

A* Search

Greedy Best-First Search (GBFS)

Heuristics:

Manhattan Distance

Euclidean Distance

Dynamic obstacle spawning

Real-time path re-planning

Performance metrics dashboard

GUI

The project uses Pygame for visualization.

Features:

Mouse-based obstacle placement

Algorithm and heuristic selection

Dynamic mode toggle

Animated agent movement

 Installation

Install dependencies:

pip install pygame
 How to Run
python main.py
 Controls

Left Click → Add wall

Right Click → Remove wall

Start Button → Run algorithm

Reset Button → Reset grid

 Configuration

At startup, you can set:

Grid size (rows & columns)

Obstacle density

 Metrics

Nodes Visited

Path Cost

Execution Time

 Dynamic Mode

Random obstacles appear during execution

Agent re-plans path automatically if blocked

 Project Structure
main.py
README.md
 Author

Course: AI 2002 – Artificial Intelligence

Assignment: Assignment 2 (Question 6)
