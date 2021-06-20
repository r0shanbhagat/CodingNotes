## **Problem: Number of Provinces.**

Lets Code Problem:
https://leetcode.com/problems/number-of-provinces/

There are n cities. Some of them are connected, while some are not. If city a is connected directly with city b, and city b is connected directly with city c, then city a is connected indirectly with city c.

A **province** is a group of directly or indirectly connected cities and no other cities outside of the group.

You are given an n x n matrix isConnected where isConnected[i][j] = 1 if the ith city and the jth city are directly connected, and isConnected[i][j] = 0 otherwise.

Return the total number of **provinces**.

Example 1:
![enter image description here](https://assets.leetcode.com/uploads/2020/12/24/graph1.jpg)
Input: isConnected = [[1,1,0],[1,1,0],[0,0,1]]
Output: 2

Example 2:
![enter image description here](https://assets.leetcode.com/uploads/2020/12/24/graph2.jpg)
Input: isConnected = [[1,0,0],[0,1,0],[0,0,1]]
Output: 3

Constraints:
1 <= n <= 200
n == isConnected.length
n == isConnected[i].length
isConnected[i][j] is 1 or 0.
isConnected[i][i] == 1
isConnected[i][j] == isConnected[j][i]

## **Solution:**

        class Solution {
        public int findCircleNum(int[][] isConnected) {
           return friendCircles(isConnected, isConnected.length);
        }
        
        static void DFS (int[][] friends, int n, int[] visited, int v) {
        for (int i = 0; i < n; ++i) {
    
            // A student is in the friend circle if he/she is friends with the student represented by
            // studentIndex and if he/she is not already in a friend circle
            if (friends[v][i] == 1 && !(visited[i]==1) && !(i == v)) {
                visited[i] = 1;
                DFS(friends, n, visited, i);
            }
        }
      }
    
      static int friendCircles(int[][] friends, int n) {
        if (n == 0) {
            return 0;
        }
     
        int numCircles = 0;     //Number of friend circles
        
        //Keep track of whether a student is already in a friend circle
        int visited[] = new int[n];
    
        for (int i=0;i < n; i++){
          visited[i] = 0;
        }
        
        //Start with the first student and recursively find all other students in his/her
        //friend circle. Then, do the same thing for the next student that is not already
        //in a friend circle. Repeat until all students are in a friend circle. 
        for (int i = 0; i < n; ++i) {
            if (!(visited[i] ==1)) {
                visited[i] = 1;
                DFS(friends, n, visited, i); //Recursive step to find all friends
                numCircles = numCircles + 1;
            }
        }
        return numCircles;
      }
    }
