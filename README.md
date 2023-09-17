# SPICE simulation in Python

This is a documentation sort-of for [my](https://github.com/savar95x/) (ee22b142, savar's) submission for the Simulation Program with Integrated Circuit Emphasis in Python, Assignment 2.

## Blueprint
I have implemented SPICE using the <b>M</b>odified <b>N</b>odal <b>A</b>nalysis (MNA)<br>
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
G is a square matrix of order (number of nodes). B is of order (number of nodes)x(number of independent voltage sources), C is the transpose of B, and D remains empty (it deals with dependent sources, which we have been asked to ignore in this assginment)<br><br>
B matrix is a vertical matrix, with the values of independent sources and voltage sources in this fashion:<br>

        [ x1 ]
        [ x2 ]
    B = [ x3 ]
        [ y1 ]
        [ y2 ]

where:<br>
xi is the sum of values of independent current sources entering(+) and leaving(-) the node i, and yi is the value of i'th independent voltage source.<br><br>
X matrix is:<br>

        [ x1 ]
        [ x2 ]
    X = [ x3 ]
        [ y1 ]
        [ y2 ]

where:<br>
xi is the voltage at i'th node. And yi is the current across the i'th independent voltage source.

## Code Explaination
The `evalSpice()` function starts with
1. calling the `ckt_list()` function, which parses the given file and returns a neat list of ckt elements. It also goes through the error cases relevent over here.
2. then, it solves for X vector, using `numpy.linalg.solve(a_matrix(ckt), z_matrix(ckt))`. I have created functions whereever felt necessary and tried to keep the code organised, but somehow the matrices function ended up being a mess. They still work though.<br>
Also, some functions such has `get_numbers_from_end()` (which gets the number from the end of a string) have been made and used to make the code more compatible (and extensible).
3. Lastly, it arranges the solved values for x_matrix in a dictionary format, and returns the (voltage at node) and (current across independent voltage sources).

## References
1. Extensive help was taken from [chatGPT](https://chat.openai.com) for string operations (mostly slicing, removing, sorting etc) because of time constraints (I started on the last day), learning about new, for me, but actually common inbuilt python functions (like sort(), split(), strip()), and for debugging particular pieces of code.
2. A big thanks to Pradeep (ee22b055), my roommate, for explaining me the basic working of MNA, and also for helping me debug the code in the last moment. We coded continuously for 18 hours from 6pm 16 Sept. IST till 12pm 17 Sept. IST, and we couldn't have gone through that without each other's company. Just to be clear, our approach was similar and the final code also looked very similar, even though we did not directly copy from each other.
3. Some references I used to learn MNA properly: [nptel video](https://www.youtube.com/watch?v=BQKVCrJfp9E), [swarthmore article on basic MNA](https://lpsa.swarthmore.edu/Systems/Electrical/mna/MNA2.html)
