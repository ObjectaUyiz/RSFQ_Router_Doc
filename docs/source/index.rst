Welcome to RSFQ_Router's documentation!
===========================================

**RSFQ_Router** is a C++ based project for gates routing & placement under the RSFQ technology node. This Document includes details of this router, from the base algorithm to module division and function definition, etc.

**characteristic of RSFQ routing**: 
-----------------------------------
   1. *only routing within one layer*, like drawing picture on a canvas, each point on the canvas can have a cross point, *which represent 2 different resources: HorizontalResource and VerticalResource*
   2. *Routing along with placement*
   3. *levelized gates*, becuase of the characteristic of RSFQ, it requres when a wire needs to cross level to connect to another gate, it must pass a gated passing gate first, which means when we doing the routing, we are facing level by level routing, for one level we only need care about a signle level, and repeat for every level and don't need any information from previous level, it can also called *level-independence*. 
   4. *each element can represent simply by a box, wire-connection is a serials connected passing boxes*
  

**Innovation**:
----------------
   1. Because of the levelize characteristic, I implenment two different canvas, one is for every level routing, and one is for all routed-level, which is the finallized routing and Cells.

      1. The *advantage* of having **level-routing-grid** is we can change the level-canvas *freely* and **without worry about the relative position of the Cell at the previous level**, after each level, we simply attach this level-canvas to the end of the Grid-canvas

   2. Use priorityBFS & Maze combine to find the shortest path without conflict
   3. If 2 nodes cannot find path within one level, we will extend the size of that level and re-run entire level
   4. Inorder to prevent one line cross all vertical resource for start & end, we try to first route horizontally

**WhyMAZE?**:
-------------
   Because all element in the RSFQ are squres, thus the most easy way to place element into canvas is using gridboard, *each gird represent the smallest element*, usually is the passing block, **larger blocks occupy an area consists by small grid nodes which no resources can use**, then Maze and BFS is the best candidate. Base on that thinking, the question is much like we place Cells onto the board, then find path between two grid we want to connect. And also because the levelized cells, for each cell level, we use a small gridboard specific for this level, and then:
      1. place all single level cells left-aligned, and create a gridboard with: 

         - **((largest width of left side cells) + (fixed width track number of routing space) + (largest width of right side cells)) * ((the larger height between    left and right cells list) + (total space between vertical cells))**
      
      2. try to place cells on the gridboard, and routing path. If routing failed, reconfig the samll gridboard and re-run the step 2
      3. after successfully finish routing one-level, place the result onto the overall Grid Canvas, then repeat from step 1 until all cells are routed

   .. code_block::
      :caption: Algorithm flow

         input: levelized cells
         input: inter-connection between cells
         if (still have level to route)
         try do {
            cell-list := all cells from one level;
            connection-list := if(not first level) {all connection for this level and the leve before} else {all connection between this and next level}
            current-level-grid-board := ((largest width of left side cells) + (fixed width track number of routing space) + (largest width of right side cells)) * 
                                          ((the larger height between left and right cells list) + (total space between vertical cells))
            if(connection-list.size not 0)
            try do{
               bool success = connect the most top of pair of points
               if(!success) put connection into faild-list
               if(faild-list.size larger threshold) reconfig current-level-grid-board, size it bigger, rerun current level
               if(success) attach current-level-grid-board to GridCanvas
            }
         }


.. note::
   - The project&document is under active development
   - **Current upadte** finished node2node routing path find by using BFS&Maze algorithm, plan the entire project by division modules and functions

**implementation**
---------------------
.. toctree::
   Grid
   Router
   Develop_log_Jan_10
