# GiftingGroups problem
### Problem statement

Amazon is working on grouping people in audible groups. You are given a list of integers which are pictorially repesented as 2D matrix

**Input List**  
110, 110, 001

**Return the number of groups
public int groups(List users){
}**

Matrix representation  
col 0 col1 col2  
row 0 **1 1 0**  
row 1 **1 1 0**  
row 2 **0 0 1**

M[i][j] = 1 represents user a and user b are connected. Each user knows himself  
For instance in above example user 0 knows user 0 and 1 so(matrix[0][0] = 0 and matrix[0][1] =1)  
Similaraly user 1 knows user 0 and 1so(matrix[1][0] = 0 and matrix[1][1] =1)  
user 2 knows no one so matrix[2][2] = 2  
Find the number of groups. in this example there are 2 groups {0,1} and {2}

When I saw the question in first pass this seems like number of island question but there was a variation which I didn't pay attention to. The question also said users can be directly known to each other or transitively.

Consider below example which was hidden test case

Matrix representation  
col 0 col1 col2 col3  
row 0 1 1 0 0  
row1 1 1 0 1  
row2 0 0 1 0  
row3 0 0 0 1

In above case the expected grouping is user 0 knows user 0(himself) and 1  
User 1 knows user 0, 1 and in addition knows user 3 since matrix[1][3] = 1 . User 3 is connected to user 1 directly and since user 0 and 1 are connected already, user 3 and user 0 are connected transitively .

In this case also the expected output is 2 groups {0,1,3} and {2} 



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

        import java.util.Arrays;  
    import java.util.List;  
      
    public class GiftingGroups {  
      
        public static void main(String[] args) {  
      
            String given1[] = {"110", "110", "011"}; //2  
      String given2[] = {"1100", "1101", "0010", "0010", "0001"}; //2  
      String given3[] = {"110", "111", "011"}; //1  
      
      
      String arr1[] = {"1100", "1110", "0110", "0001"};//2  
      String arr2[] = {"10000", "01000", "00100", "00010", "00001"};//5  
      String arr3[] = {"1100", "1101", "0010", "0010", "0001"};//2  
      String arr4[] = {"1100", "1101", "0010", "0010", "0001"};//2  
      String arr5[] = {"11100", "11001", "10100", "00011", "01011"};//1  
      String arr6[] = {"11100", "11100", "11100", "00011", "00011"};//2  
      String arr7[] = {"10100", "01010", "10100", "01010", "00001"};//3  
      
      List<String> arrayList = Arrays.asList(given3);  
     int result = findSubscriberGroups(arrayList);  
      System.out.println(result);  
      
      }  
      
        public static int findSubscriberGroups(List<String> arrayList) {  
            if (null == arrayList || arrayList.isEmpty()) {  
                return 0;  
      }  
            int count = 0;  
     int[][] isConnected = new int[arrayList.size()][arrayList.size()];  
      
     for (int i = 0; i < arrayList.size(); i++) {  
      
                String row = arrayList.get(i);  
      
     for (int j = 0; j < row.length(); j++) {  
      
                    // isConnected[i][j] = (row.charAt(j) - '0'); //Working  
      isConnected[i][j] = Integer.parseInt(Character.toString(row.charAt(j)));  
      }  
      
            }  
      
            boolean[] isReached = new boolean[isConnected.length];  
     for (int i = 0; i < isConnected.length; i++) {  
                if (!isReached[i]) {  
                    alignedGroups(isConnected, isReached, i);  
      count++;  
      
      }  
      
            }  
            return count;  
      
      }  
      
        private static void alignedGroups(int[][] isConnected, boolean[] isReached, int v) {  
            isReached[v] = true;  
      
     for (int i = 0; i < isConnected.length; i++) {  
                if (isConnected[v][i] == 1 && !isReached[i])  
                    alignedGroups(isConnected, isReached, i);  
      
      }  
      
        }  
    }

Reference url:https://www.educative.io/edpresso/the-friend-circle-problem
