
## **Problem: Find Fraudulent Activity from Logs**
A Company parses **logs of online store** user **transactions/activity to flag fraudulent activity.**
The log file is represented as an **Array** of arrays. The arrays consist of the following data:
[ <# of transactions>]
For example:
[sender_Id,recipietId,Amount]
[345366 89921 45] 

Note: the data is space delimited
So, the log data would look like:
[  
[345366 89921 45],  
[029323 38239 23]  
...  
]  
Write a function to parse the log data to find distinct users that meet or cross a certain threshold.

The function will take in 2 inputs:  
logData: Log data in form an array of arrays

threshold: threshold as an integer

Output:  
It should be an array of userids that are sorted.

If same userid appears in the transaction as userid1 and userid2, it should count as one occurrence, not two.

Example:  
Input:  
logData:

[  
[345366 89921 45],  
[029323 38239 23],  
[38239 345366 15],  
[029323 38239 77],  
[345366 38239 23],  
[029323 345366 13],  
[38239 38239 23]  
...  
]  
threshold: 3

Output: [345366 , 38239, 029323]  
Explanation:  
Given the following counts of userids, there are only 3 userids that meet or exceed the threshold of 3.

345366 -4 , 38239 -5, 029323-3, 89921-1

## **Solution:**

    import java.util.*;  
      
    class Solution {  
      
        static List<String> processLogs(List<String> logs, int threshold) {  
      
            Map<String, Integer> map = new HashMap<>();  
     for (String val : logs) {  
                String[] log = val.split("  ");  
      //Incrementing the count value  
      map.put(log[0], map.getOrDefault(log[0], 0) + 1);  
     if (!log[0].equals(log[1])) {  
                    map.put(log[1], map.getOrDefault(log[1], 0) + 1);  
      }  
            }  
      
            System.out.println(map);  
      
      
      List<String> userId = new ArrayList<>();  
     for (Map.Entry<String, Integer> entry : map.entrySet()) {  
                if (entry.getValue() >= threshold) {  
                    userId.add(entry.getKey());  
      }  
            }  
      
            Collections.sort(userId, Comparator.comparingInt(Integer::parseInt));  
      
      //return userId.toArray(new String[userId.size()]);  
      return userId;  
      }  
      
      
        public static void main(String[] args) {  
            int threshold=2;  
      List<String> input = new ArrayList() {{  
                //sender_ID,recipietID,Amount  
      add ("88 99 200");  
      add ("88 99 300");  
      add ("99 32 100");  
      add ("12 12 15");  
      
      }};  
      
      processLogs(input, threshold).forEach(System.out::println);  
      }  
    }

## Explanation
- According to problem statement  we have ???senderId recipientId Amount??? ,to solve this while accessing the logs list we need to maintain the map which contains the distinct sender , recipient (as **Key)** and transaction count (as value) for corresponding sender/recipient. 

- We???re going to update the ???transaction Count??? if we found the particular user 		involved in any transaction (while accessing the logs).
   **map.put(log[0], map.getOrDefault(log[0], 0) + 1);**
  If senderId==recipientId we???r going  to treat that transaction as single transaction and count will be not increased!!
  
 - Once  we have the sender , recipient  list and their total transaction count  we???re going to compare the count value against the Threshold value and  it???s matches we???re adding in list suspecting that user transaction is suspicious.

- At last we???re going to sort the list in ascending order before returning to result.

**Order of the Algorithm**
we can have **O(N)** complexity to filter out all the user ids above threshold and O(KlogK) to sort the filters user id. K is the result size and K <= N. Althought we have O(NlogN) in worst case scenario,

LetsCode Discussion Forum:https://leetcode.com/discuss/interview-question/989768/amazon-oa-2020-transaction-logs
