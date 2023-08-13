# 211.-Design-Add-and-Search-Words-Data-Structure


`````py
class WordDictionary:
    class TrieNode:
        def __init__(self):
            self.children = {}
            self.endofword = False

    def __init__(self):
        self.root = self.TrieNode()

    def addWord(self, word: str) -> None:
        cur = self.root 
        for ch in word:
            if ch in cur.children:
                cur = cur.children[ch]
            else:
                node = self.TrieNode()
                cur.children[ch] = node
                cur = node 
        cur.endofword  = True 

    def search(self, word: str) -> bool:
        return self.search_rec(word, self.root, 0)

    def search_rec(self, word:str, root:TrieNode, position: int) -> bool:
        if position == len(word):
            return root.endofword
        cur = root
        flag = False 

        # without this keyError p will throw
        if word[position] != '.' and word[position] not in cur.children:
            return False 

        if word[position] != '.':
            return self.search_rec(word, cur.children[word[position]], position+1)
        else:
            for c in cur.children:
                flag = flag or self.search_rec(word, cur.children[c], position+1)
            return flag 

# Your WordDictionary object will be instantiated and called as such:
# obj = WordDictionary()
# obj.addWord(word)
# param_2 = obj.search(word)
`````
