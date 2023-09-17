# SPICE simulation in Python

This is [my](https://github.com/savar95x/) (Savar Verma, EE22B142) submission for the Simulation Program with Integrated Circuit Emphasis in Python, Assignment 2.

- Blueprint
I have implemented SPICE using <b>M</b>odified <b>N</b>odal <b>A</b>nalysis (MNA)<br>
The way I went around it is making a matrix equation `AX=B`, and then solving for the X vector (using numpy).
The A matrix is the combination of conductance(G), and node voltage(B) matrices in this fashion:<br>
(Let's say the (num of nodes) = 3 and (num of independent voltage sources) = 2)

        [      |    ]                   
        [   G  | B  ]        [ x x x ]        [ x x ]
    A = [      |    ]    G = [ x x x ]    B = [ x x ] C = [ x x x ] D = [ x x ]
        [ ---- | -- ]        [ x x x ]        [ x x ]     [ x x x ]     [ x x ]
        [   C  | D  ]                    
        [      |    ]                    

where:<br>
G is a square matrix of order (number of nodes). B is of order (number of nodes)x(number of independent voltage sources), C is the transpose of B, and D remains empty (it deals with dependent sources, which we have been asked to ignore in this assginment)
