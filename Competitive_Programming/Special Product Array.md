# <p align="center"> Problem Statement<p>
# <p>Given a list of integers nums, return a new list such that each element at index i of the new list is the product of all the numbers in the original list except the one at i. Do this without using division.</p>
## Algorithm :-
### 1.The idea is to form two lists, prefix and suffix. 
### 2.In prefix, for every i, prefix[i] will be the product of all the elements in nums from index 0 to i. In suffix, for every i, suffix[i] will be the product of all the elements in nums from index n-1(n is length of nums) to 0. 
### 3.Now for every i the ans can be prefix[i - 1] * suffix[i + 1].
### 4.For the prefix list, we initialize prefix[0] = nums[0] and then traverse the nums list from index 1 till last and for every i, prefix[i] = prefix[i - 1] * nums[i]. 
### 5.For the suffix list, we initialize suffix[n-1] = nums[n-1] and then traverse the nums list from index n-2 till 0 and for every i, suffix[i] = suffix[i + 1] * nums[i]. 
### 6.Now we form a new list ans and for every i, ans[i] = prefix[i - 1] * suffix[i + 1] except for first and last index for which ans is ans[i] = suffix[i + 1] and ans[i] = prefix[i - 1] respectively.
## An Example:-
### nums = [1,2,3,4,5]
### prefix = [1,2,6,24,120]
### suffix = [120,120,60,20,5]
### Now for i=2, ans should be - 1 * 2 * 4 * 5=40
### ans[2] = prefix[2-1] * suffix[2+1]
### ans[2] = prefix[1] * suffix[3]
### ans[2] = 2 * 20 = 40
## Implementation:-
```c++
vector<int> solve(vector<int>& nums) {
    int n = nums.size();
    vector<int> prefix(n);
    vector<int> suffix(n);
    prefix[0] = nums[0];
    suffix[n - 1] = nums[n - 1];
    for (int i = 1; i < n; i++) {
        prefix[i] = prefix[i - 1] * nums[i];
    }
    for (int i = n - 2; i >= 0; i--) {
        suffix[i] = suffix[i + 1] * nums[i];
    }
    vector<int> ans(n);
    for (int i = 0; i < n; i++) {
        if (i == 0) {
            ans[i] = suffix[i + 1];
        } else if (i == n - 1) {
            ans[i] = prefix[i - 1];
        } else {
            ans[i] = prefix[i - 1] * suffix[i + 1];
        }
    }
    return ans;
}
```
## Time Complexity:-
### O(n) We traverse the nums list 3 times, each time n elements.O(n) We traverse the nums list 3 times, each time n elements.
## Space Complexity:-
### O(n) We use three auxiliary memory, each with n elements
  
