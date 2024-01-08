Router
=======
**description**:
    **Router** is the core to do the routing, 


RoutingNode
-------------
**description**: routing node is the same as GridNode and in routing algorithm, we are actually using GridRoutingNodeVector's element as routing node to drawing the line and making the mark

Path
-------------
Structure Element
^^^^^^^^^^^^^^^^^
    - **StartPos**: *(std::vector<uint32_t>)* the start point of the path, usually the start point is *within* the Cell itself
    - **TargetPos**: *(std::vector<uint32_t>)* the start point of the path, usually the target point is *within* the Cell itself
    - **RoutedPath**: *(std::vector<std::vector<uint32_t>>)* a collection of *{_y,_x}*, coordinate of *GridRoutingNodeVector*

RouterClass
-------------
Class Element
^^^^^^^^^^^^^^^^^
    - **Nodes2Explore**: *(std::priority_queue<std::vector<uint32_t>>)* used to store all nodes next to explore when finding path
    - **RoutedPathCollect**: *(std::vector<Path>)*
    - **RouterGrid**: *(Grid)* The canvas for routing program use
Class Function
^^^^^^^^^^^^^^^^
    - ``uint8_t Routing2Nodes(const std::vector<uint32_t> Start, const std::vector<uint32_t> End, const std::vector<uint32_t> CellPos, const Cell& CurrentCell);``
        - **description**:
            - This function is used within the RoutingALevel function, which routes two specific points by using BSF&Maze routing.
        - **Parameter**:
            - *Start*, *(std::vector<uint32_t>)*: 2 uint32_t represent the start point of the routing algorithm, this two point actually within the cell
            - *End*, *(std::vector<uint32_t>)*: 2 uint32_t represent the ending point of the rouging algorithm, also within hte cell.
            - *CellPos*, *(std::vector<uint32_t>)*: 2 uint32_t represent the coordinate of the left top of the cell, used as pin point for a cell
            - *CurrentCell*, *(Cell)*: use to identify the cell and its width and height, combine with cellpos can draw the out shape of the cell to prevent route into cell, but also keep the flexibility of canvas itself
        - **return**:
            - *(uint8_t)*: can be used to indicate different errors if defined, as default, 0 is correct, and no errors-code predefined
    - ``uint8_t BackTrackingPath(const std::vector<uint32_t> Start, const std::vector<uint32_t> End);``
        - **description**:
            - This function is used to find the final path which found by function Routing2Nodes
        - **Parameter**:
            - *Start*, *(std::vector<uint32_t>)*: 2 uint32_t represent the start point of the routing algorithm, this two point actually within the cell
            - *End*, *(std::vector<uint32_t>)*: 2 uint32_t represent the ending point of the rouging algorithm, also within hte cell.
        - **return**:
            - *(uint8_t)*: can be used to indicate different errors if defined, as default, 0 is correct, and no errors-code predefined
    - ``uint8_t RoutingALevel(void);``
        - **description**:
            - This function is used to routing a entire level of cells
        - **Parameter**:
            - *void*: No Parameter is needed because this function will use the class parameter *RouterGrid*
        - **return**:
            - *(uint8_t)*: this parameter can be customse to identify different status of current routing, if routing error, return 255, if no more routing needs to be down return 1, if success finish current level of routing, reutrn 0;