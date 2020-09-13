# 211.-Design-Add-and-Search-Words-Data-Structure


`````C#
Problem: Design a data structure that supports adding new words and finding if a string matches 
any previously added string.

Implement the WordDictionary class:

WordDictionary() Initializes the object.
void addWord(word) Adds word to the data structure, it can be matched later.
bool search(word) Returns true if there is any string in the data structure that matches 
word or false otherwise. word may contain dots '.' where dots can be matched with any letter.

code: 

   public class WordDictionary
    {
        private TrieNode root;
        public WordDictionary()
        {
            root = new TrieNode(); 
        }

        /** Adds a word into the data structure. */
        public void AddWord(string word)
        {
            char[] wordArr = word.ToCharArray();
            TrieNode currNode = root;

            foreach(char character in wordArr)
            {
                int index = character - 'a';
                if(currNode.Children[index] == null)
                {
                    currNode.Children[index] = new TrieNode();
                }
                currNode = currNode.Children[index];
            }
            currNode.IsEndWord = true;
        }

        /** Returns if the word is in the data structure. A word could contain the dot character '.' to represent any one letter. */
        public bool Search(string word)
        {
            return Helper(word.ToCharArray(), 0, root);
        }

        private bool Helper(char[] wordCharArr, int startIdx, TrieNode currNode)
        {
            for (int i = startIdx; i< wordCharArr.Length; i++)
            {
                char currChar = wordCharArr[i];

                if(currChar == '.')
                {
                    for (int j=0; j< currNode.Children.Length; j++)
                    {
                        if(currNode.Children[j] != null &&
                            Helper(wordCharArr, i+1, currNode.Children[j]))
                        {
                            return true;
                        }
                    }
                    return false; 
                }
                else
                {
                    int index = currChar - 'a';
                    if(currNode.Children[index] == null)
                    {
                        return false;
                    }

                    currNode = currNode.Children[index];
                }
            }

            return currNode.IsEndWord;
        }
    }

    public class TrieNode
    {
        public bool IsEndWord { get; set; }
        public TrieNode[]  Children{ get; set; }

        public TrieNode()
        {
            IsEndWord = false;
            Children = new TrieNode[26];
        }
    }
`````
