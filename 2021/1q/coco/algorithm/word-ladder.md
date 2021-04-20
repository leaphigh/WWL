```java
class Solution {
    public int ladderLength(String beginWord, String endWord, List<String> wordList) {

        final int UNREACHED = 0;
        
        HashSet<String> unreachedSet = new HashSet<>(wordList);
        if (!unreachedSet.contains(endWord)) {
            return UNREACHED;
        }
        
        int ret = 1; // shortest transformation sequence
        HashSet<String> currentLevelSet = new HashSet<>();
        currentLevelSet.add(beginWord);             

        while (currentLevelSet.size() != 0 && unreachedSet.size() != 0) {
            HashSet<String> nextLevelSet = new HashSet<>();
                
            for (String word : currentLevelSet) {
                for (int i = 0; i < word.length(); i++) {
                    char[] cword = word.toCharArray();
                    for (char c = 'a'; c <= 'z'; c++) {
                        cword[i] = c;
                        String newString = new String(cword);
                        if (unreachedSet.contains(newString)) {
                            if (endWord.equals(newString)) {
                                return ret + 1;
                            }
                            unreachedSet.remove(newString);
                            nextLevelSet.add(newString);
                        }
                    }
                }
            }
            ret++;
            currentLevelSet = nextLevelSet;
        }
        
        return UNREACHED;
    }
}
```