# Encode and Decode Strings




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
