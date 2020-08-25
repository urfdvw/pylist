# [211. Design Add and Search Words Data Structure](https://leetcode.com/problems/design-add-and-search-words-data-structure/)

You should design a data structure that supports adding new words and finding if a string matches any previously added string.

Implement the WordDictionary class:

- WordDictionary() Initializes the object.
- void addWord(word) adds word to the data structure, it can be matched later.
- bool search(word) returns true if there is any string in the data structure that matches word or false otherwise. word may contain dots '.' where dots can be matched with any letter.

Example:

    Input
    ["WordDictionary","addWord","addWord","addWord","search","search","search","search"]
    [[],["bad"],["dad"],["mad"],["pad"],["bad"],[".ad"],["b.."]]
    Output
    [null,null,null,null,false,true,true,true]

    Explanation
    WordDictionary wordDictionary = new WordDictionary();
    wordDictionary.addWord("bad");
    wordDictionary.addWord("dad");
    wordDictionary.addWord("mad");
    wordDictionary.search("pad"); // return False
    wordDictionary.search("bad"); // return True
    wordDictionary.search(".ad"); // return True
    wordDictionary.search("b.."); // return True

# Solution

```python
class trie_node:
    def __init__(self):
        self.valid = False
        self.children = dict()

class WordDictionary:

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.root = trie_node()
        

    def addWord(self, word: str) -> None:
        """
        Adds a word into the data structure.
        """
        node = self.root
        for l in word:
            if l not in node.children:
                node.children[l] = trie_node()
            node = node.children[l]
        node.valid = True
        

    def search(self, word: str) -> bool:
        """
        Returns if the word is in the data structure. A word could contain the dot character '.' to represent any one letter.
        """
        return self.dc(word, self.root)
        
    def dc(self, word, node):
        if len(word) == 0:
            return node.valid
        
        if word[0] != '.':
            if word[0] not in node.children:
                return False
            return self.dc(word[1:], node.children[word[0]])
            
        # return true is there is a true, use "or"
        ans = False
        for k in node.children.keys():
            ans = ans or self.dc(word[1:], node.children[k])
        return ans
```