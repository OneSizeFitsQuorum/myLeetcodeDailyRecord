## 题目
实现一个 Trie (前缀树)，包含 insert, search, 和 startsWith 这三个操作。

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
```C++
class Trie
{
private:
	bool is_string = false;
    unordered_map<char,Trie*> children;
public:
	Trie() {}

	void insert(const string& word)//插入单词
	{
		Trie* root = this;
		for (const auto& w : word) {
            if(root->children.count(w) == 0) root->children[w] = new Trie();
			root = root->children[w];
		}
		root->is_string = true;
	}

	bool search(const string& word)//查找单词
	{
		Trie* root = this;
		for (const auto& w : word) {
			if (root->children.count(w) == 0) return false;
			root = root->children[w];
		}
		return root->is_string;
	}

	bool startsWith(string prefix)//查找前缀
	{
		Trie* root = this;
		for (const auto& p : prefix) {
			if (root->children.count(p) == 0) return false;
			root = root->children[p];
		}
		return true;
	}
};

/**
 * Your Trie object will be instantiated and called as such:
 * Trie* obj = new Trie();
 * obj->insert(word);
 * bool param_2 = obj->search(word);
 * bool param_3 = obj->startsWith(prefix);
 */
```
## 思路

每个节点利用map来索引子节点，这样子比较省内存。

可以参考此[博客](https://leetcode-cn.com/problems/implement-trie-prefix-tree/solution/shi-xian-trie-qian-zhui-shu-by-leetcode/)