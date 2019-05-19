# 最长回文子串
## 题目描述
Given a string s, find the longest palindromic substring in s. You may assume that the maximum length of s is 1000.

### Example
    Input: "babad"
    Output: "bab"
    Note: "aba" is also a valid answer.

### 暴力法复杂度为O(n3)

### 动态规划
#### 思想：
这是一道二维dp，dp[i][j]表示字符串s从i到j的子串是不是回文。
更新的状态转移方程：dp[i][j] = dp[i+1][j-1] && s[i] == s[j]
含义：如果从i+1到j-1是回文并且s[i] == s[j]相等那么dp[i][j] = 1，就是根据所包含的子串是不是回文来更新

### 中心检测法
#### 思想

    1）将子串分为单核和双核的情况，单核即指子串长度为奇数，双核则为偶数；

    2）遍历每个除最后一个位置的字符index(字符位置)，单核：初始low = 初始high = index，low和high均不超过原字符串的下限和上限；判断low和high处的字符是否相等，相等则low++、high++（双核：初始high = 初始low+1 = index + 1）；

    3）每次low与high处的字符相等时，都将当前最长的回文子串长度与high-low+1比较。后者大时，将最长的回文子串改为low与high之间的；

    4）重复执行2）、3），直至high-low+1 等于原字符串长度或者遍历到最后一个字符，取当前截取到的回文子串，该子串即为最长的回文子串。

    private static int maxLen = 0;
    
    private static String sub = "";
    
    public static String longestPalindrome(String s) {
            if(s.length() <= 1)
                return s;
    
            for(int i = 0;i < s.length()-1;i++){
    
                findLongestPalindrome(s,i,i);//单核回文
    
                findLongestPalindrome(s,i,i+1);//双核回文
            }
            return sub;
        }
        public static  void findLongestPalindrome(String s,int low,int high){
            while (low >= 0 && high <= s.length()-1){
                if(s.charAt(low) == s.charAt(high)){
                    if(high - low + 1 > maxLen){
                        maxLen = high - low + 1;
                        sub = s.substring(low , high+1);
                    }
                    low --;//向两边扩散找当前字符为中心的最大回文子串
                    high ++;
                }
                else
                    break;
            }
        }



### 马拉车算法

