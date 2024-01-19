Design_simplify_jan_18
=========================


**Simplify**:
-----------------
    - For each cell, only left side and right side has ports
    - Each routing path from left to right

**Consequences**:
-----------------
    1. For cell port index:

        .. code-block::

            input: cell_index, cell width, cell port number
                get_cell_letop_position(cell_index): _x, _y
                    port_x = _x + cell_width
                    port_y = _y + port_num*interval_port
            output: cell port_x and port_y
