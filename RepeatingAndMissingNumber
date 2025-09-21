/************************************************************
* Problem: Repeating and Missing Number
*
* You are given an array of size n containing numbers from 1 to n.
* One number is repeating (appears twice) and one number is missing.
* Find both numbers.
*
* Example:
* Input: [4, 3, 6, 2, 1, 1]
* Output: Repeating = 1, Missing = 5
*
* Approaches:
* 1. Hashing Method (O(n) time, O(n) space)
* 2. Math Method (Sum & Sum of Squares, O(n) time, O(1) space)
* 3. XOR Method (Bit manipulation, O(n) time, O(1) space)
************************************************************/

#include <bits/stdc++.h>
using namespace std;

class Solution {
public:
    // ------------------ Hashing Method ------------------
    vector<int> findTwoElement_hash(vector<int>& arr) {
        int n = arr.size();
        vector<int> hash(n+1, 0);
        for (int num : arr) hash[num]++;
        
        int repeating=-1, missing=-1;
        for (int i=1; i<=n; i++){
            if (hash[i]==0) missing=i;
            if (hash[i]==2) repeating=i;
        }
        return {repeating, missing};
    }

    // ------------------ Math Method ------------------
    vector<int> findTwoElement_math(vector<int>& arr){
        long long n = arr.size();
        long long sumN = n*(n+1)/2;
        long long sumSqN = n*(n+1)*(2*n+1)/6;

        long long sum = 0, sumSq = 0;
        for(int num: arr){
            sum += num;
            sumSq += 1LL*num*num;
        }

        long long diff = sum - sumN; // x - y
        long long diffSq = sumSq - sumSqN; // x^2 - y^2
        long long sumXY = diffSq / diff;

        long long repeating = (diff + sumXY)/2;
        long long missing = repeating - diff;
        return {(int)repeating, (int)missing};
    }

    // ------------------ XOR Method ------------------
    vector<int> findTwoElement_xor(vector<int>& arr){
        int n = arr.size();
        int xorAll = 0;

        for(int i=0; i<n; i++) xorAll ^= arr[i];
        for(int i=1; i<=n; i++) xorAll ^= i;

        int setBit = xorAll & -xorAll;

        int x=0, y=0;
        for(int num : arr){
            if(num & setBit) x ^= num;
            else y ^= num;
        }
        for(int i=1; i<=n; i++){
            if(i & setBit) x ^= i;
            else y ^= i;
        }

        // Determine which is repeating
        for(int num : arr){
            if(num == x) return {x, y};
        }
        return {y, x};
    }
};

int main(){
    vector<int> arr = {4,3,6,2,1,1};
    Solution sol;

    auto ans1 = sol.findTwoElement_hash(arr);
    cout << "Hashing Method: Repeating = " << ans1[0] << ", Missing = " << ans1[1] << endl;

    auto ans2 = sol.findTwoElement_math(arr);
    cout << "Math Method: Repeating = " << ans2[0] << ", Missing = " << ans2[1] << endl;

    auto ans3 = sol.findTwoElement_xor(arr);
    cout << "XOR Method: Repeating = " << ans3[0] << ", Missing = " << ans3[1] << endl;

    return 0;
}
