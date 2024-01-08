Welcome to RSFQ_Router's documentation!
===========================================

**RSFQ_Router** is a C++ based project for gates routing & placement under the RSFQ technology node.
This Document includes details of our router, from the base algorithm to module division and function definition, etc.

**characteristic of RSFQ routing**: 
   1. *only routing within one layer*, like drawing picture on a canvas, each point on the canvas can have a cross point, *which represent 2 different resources: HorizontalResource and VerticalResource*
   2. *Routing along with placement*
   3. *levelized gates*, becuase of the characteristic of RSFQ, it requres when a wire needs to cross level to connect to another gate, it must pass a gated passing gate first, which means when we doing the routing, we are facing level by level routing, for one level we only need care about a signle level, and repeat for every level and don't need any information from previous level, it can also called *level-independence*. 

**Inovation**:
   1. Because of the levelize characteristic,I implenment two different canvas, one is for every level routing, and one is for all routed-level, which is the finallized routing and Cells.
      1. The advantage of having level-routing-grid is we can change the level-canvas freely and without worry about the relative position of the Cell at the previous level, after each level, we simply attach this level-canvas to the   end of the Grid-canvas
   2. Use priorityBFS & Maze combine to find the shortest path without conflict
   3. If 2 nodes cannot find path within one level, we will extend the size of that level and re-run entire level
   4. Inorder to prevent one line cross all vertical resource for start & end, we try to first route horizontally

**Current upadte** finished node2node routing path find by using BFS&Maze algorithm, plan the entire project by division modules and functions

.. note::
   The project&document is under active development

Table of Contents
---------------------
.. toctree::
   Grid
   Router
