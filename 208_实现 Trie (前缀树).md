## 题目
实现一个 Trie （前缀树），包含 insert, search, 和 startsWith 这三个操作。

**示例**
```
Trie trie = new Trie();

trie.insert("apple");
trie.search("apple");   // 返回 true
trie.search("app");     // 返回 false
trie.startsWith("app"); // 返回 true
trie.insert("app");   
trie.search("app");     // 返回 true
```

**说明**
* 你可以假设所有的输入都是由小写字母 a-z 构成的。
* 保证所有输入均为非空字符串。

## 代码
```Java
class Trie {

    private Node root;

    public Trie() {
        root = new Node();
    }
    
    public void insert(String word) {
        Node cur = root;
        for(char c : word.toCharArray()) {
            Node child = cur.children.get(c);
            if(child == null) {
                child = new Node();
                cur.children.put(c, child);
            }
            cur = child;
        }
        cur.hasString = true;
    }
    
    public boolean search(String word) {
        Node cur = root;
        for(char c : word.toCharArray()) {
            Node child = cur.children.get(c);
            if(child == null) {
                return false;
            }
            cur = child;
        }
        return cur.hasString;
    }
    
    public boolean startsWith(String prefix) {
        Node cur = root;
        for(char c : prefix.toCharArray()) {
            Node child = cur.children.get(c);
            if(child == null) {
                return false;
            }
            cur = child;
        }
        return true;
    }
}

class Node {
    Map<Character, Node> children = new HashMap<>();
    boolean hasString = false;
}

/**
 * Your Trie object will be instantiated and called as such:
 * Trie obj = new Trie();
 * obj.insert(word);
 * boolean param_2 = obj.search(word);
 * boolean param_3 = obj.startsWith(prefix);
 */
```

## 思路

* 时间复杂度：初始化为 O(1)，其余操作为 O(∣S∣)，其中 |S| 是每次插入或查询的字符串的长度。

* 空间复杂度：O(∣T∣⋅Σ)，其中 |T| 为所有插入字符串的长度之和，Σ 为字符集的大小，本题 Σ=26。