Develop_log_Jan_10
=======================

**Log**:
    1. I try to setup a cover of software used to contain different routing algorithm, first try Maze, base on current implementation, all algorithm part are selled in function ``Routing2Nodes`` and ``BackTrackingPath``, and the cover fucntion ``RoutingALevel`` provide setup and environment which in current level of design are common for all algorithm since we fully levelized all cells without interface with others, we can even use diffent algorithm for different level and then combine into one piece. 
    2. Need to build a directory to suit different algorithm, currently in my mind: 
        
        2.1 the first directory should contain the information about the cells, included:

            - Cell index, use to get cell information like width and height
            - Cell level, this can be included in Vector<Vector> position of that cell
            - list of cell port, each port for both cells should have unique identify ID, this can help in later routing to determining which position to place the port and how to connect the two port

        2.1 the second directory contains all constrain and connection between cells:

            - connection level
            - connection cells and corresponding ports
            - connection delay requirements
        
    3. Drawed a software flow for reference

        .. figure: ../media/flow.png
           :alt: software flow
           :align: center
           :caption: software flow