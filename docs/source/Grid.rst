Grid
========
**description**:
    **Grid** is the *canvas* for our routing program, *all element* are drawing above the **Grid**, usually the type of gridnode are either *Cell*, *RoutedNode*, and *empty GridNode*, the final output of this program is a 2-D vector consists with GridNode. 


GridNode
-----------
Structure Element
^^^^^^^^^^^^^^^^^
    - **NodeTpye**: *(enum)* one of three type: *RoutingNode, ObstacleNode, CellNode: enum type*
    - **HorizontalResource**: *(uint8_t)* the resource can use to route a path horizontally, *default value is 1*
    - **VerticalResource**:  *(uint8_t)* the resource can use to route a path vertically, *default value is 1*
    - **from**: *(enum)* when routing, use to indicate this node is passed from which direction, has 7 values: *Idle, FromLeft, FromAbove, FromBelow, FromRight, StartPo, TargetPo*

Cell
-----------
Structure Element
^^^^^^^^^^^^^^^^^
    - **NodeTpye**: *(enum)* *CellNode*
    - **CellWidth_X**: *(uint16_t)* Width of the Cell
    - **CellWidth_Y**: *(uint16_t)* Height of the Cell

GridClass
-----------
Class Element
^^^^^^^^^^^^^^^^^
    - **GridNodeBoard**: *(std::vector<std::vector<GridNode>>)*, private, used to place all the layers that have finished routing
    - **GridRoutingNodeVector**: *(std::vector<std::vector<GridNode>>)*, public, used for layer by layer routing
    - **VisitedNode**: *(std::vector<std::vector<bool>>)*, public, used when rouging to find path
    - **CellVector**: *(std::vector<std::vector<Cell>>)*, public, all Cells need to be routed, and the 2-d vector can better levelize all Cells base on the requirement of RSFQ technology
    - **CurrentCellRoutingLevel**: *(uint8_t)*, public, this can use indicator to tell the program where we current are and if there are more levels to route
    - **MaxCellRoutingLevel**: *(uint8_t)*, public, the max level of levelized Cell array, duplicate of **CellVector[0].size()**
Class Function
^^^^^^^^^^^^^^^^
    - ``uint8_t initGridRoutingNodeVector(const uint32_t& _x, const uint32_t& _y)``
        - **description**:
            - This function is used to init the current routing layer, the cell is placed outside the area, but the area of the routing node should have space reserve for the Cell because it can prevent irregular shape of the Vector
        - **Parameter**
            - *_x*, *(uint32_t)*: the width of the vector area been used for grid, default value is 5
            - *_y*, *(uint32_t)*: the height of the vector area, usually the height of the current layer cells with gaps between cells, Cells are identify by the empty sapce, which means if two cell are connect without extra row will be identify as single cell.
        - **return**
            - *(uint8_t)*: can be used to indicate different errors if defined, as default, 0 is correct, and no errors-code predefined
    - ``uint8_t initCellVector(std::vector<std::vector<Cell>> CellVector);``
        - **description**:
            - This function is used to load all the Cells which needs to be routed and the 2-D dimension represent the relative relation between different Cells, also diterming the total level of cells we need to route
        - **Parameter**:
            - *CellVector*, *(std::vector<std::vector<Cell>>)*: 2-D dimension Cell node vector contains all cells and realtion between Cells, this is a levelized Cell directory
        - **return**:
            - *(uint8_t)*: can be used to indicate different errors if defined, as default, 0 is correct, and no errors-code predefined
