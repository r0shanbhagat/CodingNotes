# The friend circle problem

### Problem statement

There are  _N_  students in a class. Some of them are friends,others are not. Their friendship is transitive; if A is a  _direct_  friend of B, and B is a  _direct_  friend of C, then A is an  _indirect_  friend of C. A friend circle is defined as a group of students who are  _direct_  or  _indirect_  friends.

The input matrix will have a number of rows and columns equal to the number of students in a class. A cell  `[i,j]`  will hold the value  **1**  if student  `i`  and student  `j`  are friends; otherwise, the cell will hold the value  **0**. For example, if the input is:

012301100111102011030001

Then there are  **2**  friend circles. Student  **0**  is friends with student  **1**  _only_, but student 1 is friends with  _both_​ student  **0**  and student  **2**. These three students make one friend circle. Student  **3**, alone, makes another friend circle.

Similarly, if the input matrix is:

012301100111002001030001

Then there are three friend circles. Student  **0**  and student  **1**  are only friends with each other, so they make one friend circle. Student  **2**  and student  **3**  don’t have any friends, so they each make one friend circle.

Let’s try to solve this for  _any_  value of  **n**.

> Note that the input matrix will always be  _symmetric_  because the friendship is transitive.

We can try to think of the symmetric input matrix as an  _undirected_  graph. Let’s make an undirected graph for our first example:

![svg viewer](https://www.educative.io/api/edpresso/shot/6581624198135808/image/5618405807751168)

​Notice that all friends (both direct and indirect), who should be in one friend circle are also in one  _connected component​_  in the graph.

> The  **number of connected components in the graph**  will give us the number of friend circles in the class.

### Algorithm

We can treat our input matrix as an  **adjacency matrix**; our task is to find the number of connected components. Here are the steps:

-   Initialize a list/array,  `visited`, to keep track of visited vertices of size  **n**  with  **0**  as the initial value at each index.
-   For every vertex  `v`, if  `visited[v]`  is 0, traverse the graph using  `DFS`; else, move to the next  `v`.
-   Set  `visited[v]`  to  **1**  for every  `v`  that the DFS traversal encounters.
-   When the  `DFS`  traversal terminates, increment the friend circles counter by  **1**  as it means that​ one whole connected component has been traversed.
### Code
The following code snippet implements the above algorithm:

    class friendCircle {  
      
        static void DFS(boolean[][] friends, int n, boolean[] visited, int v) {  
            for (int i = 0; i < n; ++i) {  
                // A student is in the friend circle if he/she is friends with the student represented by  
     // studentIndex and if he/she is not already in a friend circle  if (friends[v][i] == true && !visited[i] && i != v) {  
                    visited[i] = true;  
      DFS(friends, n, visited, i);  
      }  
            }  
        }  
      
        static int friendCircles(boolean[][] friends, int n) {  
            if (n == 0) {  
                return 0;  
      }  
      
            int numCircles = 0; //Number of friend circles  
      
     //Keep track of whether a student is already in a friend circle  boolean visited[] = new boolean[n];  
      
     for (int i = 0; i < n; i++) {  
                visited[i] = false;  
      }  
      
            //Start with the first student and recursively find all other students in his/her  
     //friend circle. Then, do the same thing for the next student that is not already //in a friend circle. Repeat until all students are in a friend circle. for (int i = 0; i < n; ++i) {  
                if (!visited[i]) {  
                    visited[i] = true;  
      DFS(friends, n, visited, i); //Recursive step to find all friends  
      numCircles = numCircles + 1;  
      }  
            }  
      
            return numCircles;  
      }  
      
        public static void main(String args[]) {  
            int n = 4;  
     boolean[][] friends = {  
                    {true, true, false, false},  
      {true, true, true, false},  
      {false, true, true, false},  
      {false, false, false, true}  
            };  
      System.out.println("Number of friends circles: " + friendCircles(friends, n));  
      }  
      
    }

Reference url:https://www.educative.io/edpresso/the-friend-circle-problem
