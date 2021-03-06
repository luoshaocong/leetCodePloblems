#  LeetCode algorithm problems set



## Problem 1

Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

Examples
```
Input: [-2,1,-3,4,-1,2,1,-5,4],
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
```

## Answer for problem 1

```javascript
var maxSubArray = function(nums) {
  const hash = { 0: nums[0]}
  let max = nums[0];

  for (let i = 1; i < nums.length; i += 1) {
    hash[i] = Math.max(hash[i - 1] + nums[i], nums[i]);
    max = Math.max(hash[i], max);
  }

  return max;
};
```


## Problem 2
Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

Examples

```
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```
## Answer for problem 2


Time complexity:O(n).
Space complexity:O(n).
```javascript


function twoSum(nums, target) {
  var twoSum = [];
  nums.forEach((num, i) =>{
    var diff = target - num;
    var j = nums.indexOf(diff)
    if (j > -1 && j !== i) {
       twoSum[0] = i;
       twoSum[1] = j;
       return true;
    }
  })
  return twoSum;
}

```


## Problem 3


You are climbing a stair case. It takes n steps to reach to the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

Note: Given n will be a positive integer.

Example 1:
```

Input: 2
Output: 2
Explanation: There are two ways to climb to the top.
1. 1 step + 1 step
2. 2 steps

```
Example 2:
```

Input: 3
Output: 3
Explanation: There are three ways to climb to the top.
1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step
```
## Answer for problem 3


```javascript

var climbStairs = function(n, memo = {}) {
    if(n <= 1) return 1;

    memo[n] = memo[n] || climbStairs(n-1, memo) + climbStairs(n-2, memo);

    return memo[n];
};

```

## Problem 4

Given a non-empty array of integers, every element appears twice except for one. Find that single one.

## Answer for problem 4
```javascript
var singleNumber = function(nums) {
  nums.sort();
  for(i = 0; i < nums.length; i++){
    if(i %2 === 0 && nums[i]!== nums[i+1]){
      return nums[i];

    }
  }
};
```
## Problem 5
Given an integer array, you need to find one continuous subarray that if you only sort this subarray in ascending order, then the whole array will be sorted in ascending order, too.

You need to find the shortest such subarray and output its length.

Example 1:
```
Input: [2, 6, 4, 8, 10, 9, 15]
Output: 5
Explanation: You need to sort [6, 4, 8, 10, 9] in ascending order to make the whole array sorted in ascending order.
```

## Answer for problem 5
```javascript
var findUnsortedSubarray = function(nums) {
    cpy = nums.slice();
    nums.sort((a,b)=>{return a-b});
    start = 0;
    end = 0;   
    for(i = 0; i < nums.length; i++) {
        if(nums[i]!==cpy[i]) {
            start = i;
            break;
        }
    }
    for(j = nums.length; j>1 ; j--) {
      if(nums[j]!==cpy[j]) {
          end = j;
          break;
       }       

    }
    return j - i+1 ;
};
```

## Problem 6
Given a string, your task is to count how many palindromic substrings in this string.

The substrings with different start indexes or end indexes are counted as different substrings even they consist of same characters.

Example 1:
```
Input: "abc"
Output: 3
Explanation: Three palindromic strings: "a", "b", "c".
```
Example 2:
```
Input: "aaa"
Output: 6
Explanation: Six palindromic strings: "a", "a", "a", "aa", "aa", "aaa".
```
## Answer for problem 6
```javascript
var countpalindromic = function(i,j,s) {
  count = 0;
  while(i >= 0 && j < s.length && s[i] === s[j]){
    count++;
    i--;
    j++;

  }
  return count;
};


var countSubstrings = function(s) {
  count = s.length;

  for(i = 0; i < s.length; i++){
    count += countpalindromic(i,i + 1,s) + countpalindromic(i, i+2, s);


  }

    return count;
};
countSubstrings("abba")




```

## Answer for problem 7

Write a program that outputs the string representation of numbers from 1 to n.

But for multiples of three it should output “Fizz” instead of the number and for the multiples of five output “Buzz”. For numbers which are multiples of both three and five output “FizzBuzz”.

Example:
```
n = 15,

Return:
[
    "1",
    "2",
    "Fizz",
    "4",
    "Buzz",
    "Fizz",
    "7",
    "8",
    "Fizz",
    "Buzz",
    "11",
    "Fizz",
    "13",
    "14",
    "FizzBuzz"
]
```
## Answer for problem 7

```javascript
var fizzBuzz = function(n) {
 arr = []
 for(i = 1; i <=15; i++) {
    if(i % 3 === 0 && i % 5 === 0) {
         arr.push("fizzBuzz");

     }
     else if(i % 3 === 0) {
       arr.push("fizz");
    }
      else if(i % 5 === 0) {
       arr.push("buzz");
     }
     else {
         arr.push(i.toString());;
     }

 }
 return arr;


};

fizzBuzz(15)
```


## Question for problem 8
Consider all the leaves of a binary tree.  From left to right order, the values of those leaves form a leaf value sequence.



For example, in the given tree above, the leaf value sequence is (6, 7, 4, 9, 8).

Two binary trees are considered leaf-similar if their leaf value sequence is the same.

Return true if and only if the two given trees with head nodes root1 and root2 are leaf-similar.


## Answer for problem 8
```javascript

var leafSimilar = function(root1, root2) {
    return helper(root1)===helper(root2);
};


var helper=function(root){
    var op=[];
    inorder(root,op);
    return op.join(",");
}

var inorder=function(root,op){
  if(!root.left && !root.right){
        op.push(root.val);
    }
    inorder(root.left,op);
    inorder(root.right,op);
}
```
## Question for problem 9
Given the root node of a binary search tree (BST) and a value. You need to find the node in the BST that the node's value equals the given value. Return the subtree rooted with that node. If such node doesn't exist, you should return NULL.

For example,
```
Given the tree:
        4
       / \
      2   7
     / \
    1   3

And the value to search: 2
```
You should return this subtree:
```

      2     
     / \   
    1   3
```
In the example above, if we want to search the value 5, since there is no node with value 5, we should return NULL.

Note that an empty tree is represented by NULL, therefore you would see the expected output (serialized tree format) as [], not null.


## Answer for problem 9
```javascript

/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {TreeNode} root
 * @param {number} val
 * @return {TreeNode}
 */


searchBST = function(root,val) {
  if(val < root) {
    return searchBST(root.left,val);
  }

  else if(val > root) {
    return searchBST(root.right,val);
  }

  else if(val === root){
    return root;
  }

    else return [];
}


```

## Question for problem 10
Given a linked list, determine if it has a cycle in it.


## Answer for problem 10

Using two pointer

```javascript

var hasCycle = function(head) {

  if(head && head.next) {
    let slow = head;
    let fast = head.next;

  }
  while(slow != fast) {

    slow = slow.next;
    fast =fast.next.next;
    if(fast === NULL || fast.next === null) {
      return false;
    }  
  }
  return true;




}
```
## Question for problem 11
Write a program to find the node at which the intersection of two singly linked lists begins.


For example, the following two linked lists:
```
A:          a1 → a2
                   ↘
                     c1 → c2 → c3
                   ↗            
B:     b1 → b2 → b3
begin to intersect at node c1.
```
## Answer for problem 11
```javascript

var getIntersectionNode = function(headA, headB) {
    if(headA == null || headB ==null ){
        return null;
    }
    var hA = headA;
    var hB = headB;
    while(hA !== hB) {
        hA =hA.next;
        hB =hB.next;
        if(hA ===hB){
            return hA;
        }
        if (!hA) { hA = headB; }
        if (!hB) { hB = headA; }
    }


    return hA;

};
```
## Question for problem 12

Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).

For example, this binary tree [1,2,2,3,4,4,3] is symmetric:
```
    1
   / \
  2   2
 / \ / \
3  4 4  3
```
But the following [1,2,2,null,3,null,3] is not:
```
    1
   / \
   \   \
   3    3
```
### Answer for problem 12


```javascript
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {TreeNode} root
 * @return {boolean}
 */
 var isSymmetric = function(root) {
     const ismirror =(root1, root2) =>{
     if(root1 ==null && root2 ==null)
         return true;
     if(root1 ==null || root2 ==null)
         return false;
     return (root1.val ==root2.val)
         &&ismirror(root1.right, root2.left)
          &&ismirror(root1.left,root2,right);


 }

 }





```

## Question for problem 13

Given an array A of non-negative integers, half of the integers in A are odd, and half of the integers are even.

Sort the array so that whenever A[i] is odd, i is odd; and whenever A[i] is even, i is even.

You may return any answer array that satisfies this condition.



Example 1:
```
Input: [4,2,5,7]
Output: [4,5,2,7]
Explanation: [4,7,2,5], [2,5,4,7], [2,7,4,5] would also have been accepted.
```
### Answer for problem 13


```javascript



/**
 * @param {number[]} A
 * @return {number[]}
 */
var sortArrayByParityII = function(A) {
    var ans = [];
    var t = 0;
    for( i = 0;i < A.length; i++)
        if(A[i] % 2 === 0 ){
            ans[t] = A[i];
            t+=2;

        }
    var t = 1;
    for( i = 0;i < A.length; i++)
        if(A[i] % 2 === 1 ){
            ans[t] = A[i];
            t+=2;

        }

    return ans;

};

```
### Question for problem 14
Given a binary matrix A, we want to flip the image horizontally, then invert it, and return the resulting image.

To flip an image horizontally means that each row of the image is reversed.  For example, flipping [1, 1, 0] horizontally results in [0, 1, 1].

To invert an image means that each 0 is replaced by 1, and each 1 is replaced by 0. For example, inverting [0, 1, 1] results in [1, 0, 0].

Example 1:
```
Input: [[1,1,0],[1,0,1],[0,0,0]]
Output: [[1,0,0],[0,1,0],[1,1,1]]
Explanation: First reverse each row: [[0,1,1],[1,0,1],[0,0,0]].
Then, invert the image: [[1,0,0],[0,1,0],[1,1,1]]
```
Example 2:
```

Input: [[1,1,0,0],[1,0,0,1],[0,1,1,1],[1,0,1,0]]
Output: [[1,1,0,0],[0,1,1,0],[0,0,0,1],[1,0,1,0]]
Explanation: First reverse each row: [[0,0,1,1],[1,0,0,1],[1,1,1,0],[0,1,0,1]].
Then invert the image: [[1,1,0,0],[0,1,1,0],[0,0,0,1],[1,0,1,0]]
```
### Answer of problem 14

```javascript


var flipAndInvertImage = function(A) {
    return A.map(row => row.map(ele => ele === 0 ? 1 : 0).reverse());
};
```

### Question for problem 15

Given a binary tree, return the inorder traversal of its nodes' values.

Example:
```

Input: [1,null,2,3]
   1
    \
     2
    /
   3

Output: [1,3,2]
```

```javascript

var inorderTraversal = function(root) {
    let results = [];

    let inorder = node => {
        if(!node) return null;

        if(node.left) {
            inorder(node.left);
        }

        results.push(node.val);

        if(node.right) {
            inorder(node.right);
        }
    }

    inorder(root);

    return results;
};



```
