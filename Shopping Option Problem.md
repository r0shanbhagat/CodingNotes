## Shopping Option Problem


A customer wants to buy a pair of jeans, a pair of shoes, a skirt, and a top but has a limited budget in dollars. Given different pricing options for each product, determine how many options our customer has to buy 1 of each product. You cannot spend more money than the budgeted amount.

Example  
priceOfJeans = [2, 3]  
priceOfShoes = [4]  
priceOfSkirts = [2, 3]  
priceOfTops = [1, 2]  
budgeted = 10

The customer must buy shoes for 4 dollars since there is only one option. This leaves 6 dollars to spend on the other 3 items. Combinations of prices paid for jeans, skirts, and tops respectively that add up to 6 dollars or less are [2, 2, 2], [2, 2, 1], [3, 2, 1], [2, 3, 1]. There are 4 ways the customer can purchase all 4 items.

Function Description

Complete the getNumberOfOptions function in the editor below. The function must return an integer which represents the number of options present to buy the four items.

getNumberOfOptions has 5 parameters:  
int[] priceOfJeans: An integer array, which contains the prices of the pairs of jeans available.  
int[] priceOfShoes: An integer array, which contains the prices of the pairs of shoes available.  
int[] priceOfSkirts: An integer array, which contains the prices of the skirts available.  
int[] priceOfTops: An integer array, which contains the prices of the tops available.  
int dollars: the total number of dollars available to shop with.

Constraints

1 ≤ a, b, c, d ≤ 103  
1 ≤ dollars ≤ 109  
1 ≤ price of each item ≤ 109  
Note: a, b, c and d are the sizes of the four price arrays

## Solution1

    import java.util.ArrayList;  
    import java.util.List;  
    public class solution123 {  
        public static int shoppingOptionCount(List<List<Integer>> items, int budget) {  
            if (budget < 0)  
                return 0;  
      
     if (items.size() == 1)  
                return singleItemShoppingCount(items.get(0), budget);  
      
     int count = 0;  
     for (int p : items.get(0)) {  
                if (p <= budget) {  
                    List<List<Integer>> newItems = new ArrayList<>(items);  
      newItems.remove(0);  
      count += shoppingOptionCount(newItems, budget - p);  
      }  
            }  
            return count;  
      }  
      
        public static int singleItemShoppingCount(List<Integer> prices, int budget) {  
            int count = 0;  
     for (int p : prices) {  
                if (p <= budget)  
                    count += 1;  
      }  
            return count;  
      }  
      
        public static void main(String[] args) {  
      
            List<Integer> l1 = new ArrayList<>();  
      l1.add(2);  
      l1.add(3);  
      
      List<Integer> l2 = new ArrayList<>();  
      l2.add(4);  
      
      List<Integer> l3 = new ArrayList<>();  
      l3.add(2);  
      l3.add(3);  
      
      List<Integer> l4 = new ArrayList<>();  
      l4.add(1);  
      l4.add(2);  
      
      List<List<Integer>> l5 = new ArrayList<>();  
      l5.add(l1);  
      l5.add(l2);  
      l5.add(l3);  
      l5.add(l4);  
      
      System.out.println(shoppingOptionCount(l5, 10));  
      }  
    }

## Solution2

    import java.util.ArrayList;  
    import java.util.List;  
      
    public class shoppingList {  
    static int count=0;  
    private static void dfs(List<int []> prices, int r, int pos, int sum){  
      
        if(sum > r) return;  
     if(sum <= r && pos == prices.size()) {  
            count++;  
     return;  }  
      
        for(int x : prices.get(pos))  
        {  
            sum +=x;  
      dfs(prices, r, pos+1, sum);  
      sum -=x;  
      }  
    }  
      
    public static void main(String arg[]){  
        int p[] = new int[]{2,3};  
     int s[] = new int[]{4};  
     int t[] = new int[]{2,3};  
     int k[] = new int[]{1,2};  
     int rupee = 10;  
      
      List<int []> prices= new ArrayList<>();  
      prices.add(p);  
      prices.add(s);  
      prices.add(t);  
      prices.add(k);  
      dfs(prices, rupee, 0, 0);  
      System.out.println(count);  
    }  
    }

Forum Discussion :https://leetcode.com/discuss/interview-question/1031663/amazon-oa#
