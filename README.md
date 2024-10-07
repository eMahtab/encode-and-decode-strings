# Encode and Decode Strings
## https://leetcode.com/problems/encode-and-decode-strings

Design an algorithm to encode a list of strings to a string. The encoded string is then sent over the network and is decoded back to the original list of strings.

Machine 1 (sender) has the function:

string encode(vector<string> strs) {
  // ... your code
  return encoded_string;
}
Machine 2 (receiver) has the function:
vector<string> decode(string s) {
  //... your code
  return strs;
}
So Machine 1 does:

string encoded_string = encode(strs);
and Machine 2 does:

vector<string> strs2 = decode(encoded_string);
strs2 in Machine 2 should be the same as strs in Machine 1.

Implement the encode and decode methods.

You are not allowed to solve the problem using any serialize methods (such as eval).

 
```java
Example 1:

Input: dummy_input = ["Hello","World"]
Output: ["Hello","World"]
Explanation:
Machine 1:
Codec encoder = new Codec();
String msg = encoder.encode(strs);
Machine 1 ---msg---> Machine 2

Machine 2:
Codec decoder = new Codec();
String[] strs = decoder.decode(msg);
Example 2:

Input: dummy_input = [""]
Output: [""]
 
```
### Constraints:

1. 1 <= strs.length <= 200
2. 0 <= strs[i].length <= 200
3. strs[i] contains any possible characters out of 256 valid ASCII characters.
 

Follow up: Could you write a generalized algorithm to work on any possible set of characters?


## Implementation :
```java
public class Codec {

    // Encodes a list of strings to a single string.
    public String encode(List<String> strs) {
        if (strs == null || strs.size() < 1)
        return "";
        String separator = "#";
        String encodedString = "";
        int n = strs.size();
        for (int i = 0; i < n; i++) {
            String str = strs.get(i);
            String code = str.length() + separator + str;
            encodedString = encodedString + code;
        }
        return encodedString;
    }

    // Decodes a single string to a list of strings.
    public List<String> decode(String str) {
        List<String> strs = new ArrayList<>();
        if(str.length() == 0)
            return strs;
        int index = 0;
        while (index < str.length()) {
            String decodedString = "";
            String len = "";
            while(str.charAt(index) != '#') {
                len = len + str.charAt(index);
                index++;
            }
            index++;
            int stringLength = Integer.parseInt(len);
            if(stringLength != 0) {
                decodedString = str.substring(index, index + stringLength);
                index = index + stringLength;
            }
            strs.add(decodedString);
        }
      return strs;
   }
}

// Your Codec object will be instantiated and called as such:
// Codec codec = new Codec();
// codec.decode(codec.encode(strs));
```
