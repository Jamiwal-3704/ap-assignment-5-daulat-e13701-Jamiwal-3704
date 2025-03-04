[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/0Zzlu9gw)
# AP-ASSIGNMENT-5-DAULAT-E13701
TREE
https://leetcode.com/problems/maximum-depth-of-binary-tree/

    ```int maxDepth(TreeNode* root) {
        if(!root) return 0;
        int maxLeft = maxDepth(root->left);
        int maxRight = maxDepth(root->right);
        return max(maxLeft, maxRight)+1;
    }```
![image](https://github.com/user-attachments/assets/2e046b6e-130a-439e-9ea9-47e7460096ed)

https://leetcode.com/problems/validate-binary-search-tree/
 
 ```
void findInorder(TreeNode* root, vector<int> &inorder) {
        if (!root) return ;

        findInorder(root->left, inorder);
        inorder.push_back(root->val);
        findInorder(root->right, inorder);
    }

    bool isValidBST(TreeNode* root) {
        vector<int> inorder;
        findInorder(root, inorder);

        for (int i = 1; i < inorder.size(); i++) {
            if (inorder[i - 1] >= inorder[i]) return false;
        }

        return true;
    }
```

![image](https://github.com/user-attachments/assets/8c86bf90-1b9a-4236-800b-77792696948a)

https://leetcode.com/problems/symmetric-tree/

```
bool isMirror(TreeNode* left, TreeNode* right) {
    if (!left && !right) return true;
    if (!left || !right) return false;
    return (left->val == right->val) && isMirror(left->left, right->right) && isMirror(left->right, right->left);
}

bool isSymmetric(TreeNode* root) {
    if (!root) return true;
    return isMirror(root->left, root->right);
}
```

![image](https://github.com/user-attachments/assets/354ff45c-ff27-40e7-b93c-8bf22789bf41)

https://leetcode.com/problems/binary-tree-level-order-traversal/
```
vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>>ans;
        if(root==NULL)return ans;
        queue<TreeNode*>q;
        q.push(root);
        while(!q.empty()){
            int s=q.size();
            vector<int>v;
            for(int i=0;i<s;i++){
                TreeNode *node=q.front();
                q.pop();
                if(node->left!=NULL)q.push(node->left);
                if(node->right!=NULL)q.push(node->right);
                v.push_back(node->val);
            }
            ans.push_back(v);
        }
        return ans;
    }
```
![image](https://github.com/user-attachments/assets/d2d65cd4-7a58-48b9-9c5d-d4b4e0cc887b)

https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/
```
 TreeNode* sortedArrayToBST(vector<int>& nums) {
        return helper(nums, 0, nums.size() - 1);
    }

private:
    TreeNode* helper(vector<int>& nums, int left, int right) {
        if (left > right) return nullptr;
        int mid = left + (right - left) / 2;
        TreeNode* root = new TreeNode(nums[mid]);
        root->left = helper(nums, left, mid - 1);
        root->right = helper(nums, mid + 1, right);
        return root;
    }
```
![image](https://github.com/user-attachments/assets/a0d06f77-ce14-46d2-ad3c-4e8a851d0955)

https://leetcode.com/problems/binary-tree-inorder-traversal/

```
vector<int> inorderTraversal(TreeNode* root) {
    vector<int> ans;
    if (root == NULL) return ans;
    vector<int> left = inorderTraversal(root->left);
    ans.insert(ans.end(), left.begin(), left.end());
    ans.push_back(root->val);
    vector<int> right = inorderTraversal(root->right);
    ans.insert(ans.end(), right.begin(), right.end());
    return ans;
}
```
![image](https://github.com/user-attachments/assets/a453a1bf-3ed1-4bec-a87c-4d3e44abca25)

https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/
```
class Solution {
public:
    TreeNode* buildTree(vector<int>& inorder, vector<int>& postorder) {
        unordered_map<int, int> index;
        for (int i = 0; i < inorder.size(); i++) {
            index[inorder[i]] = i;
        }
        return buildTreeHelper(inorder, postorder, 0, inorder.size() - 1, 0, postorder.size() - 1, index);
    }
    
    TreeNode* buildTreeHelper(vector<int>& inorder, vector<int>& postorder, int inorderStart, int inorderEnd, int postorderStart, int postorderEnd, unordered_map<int, int>& index) {
        if (inorderStart > inorderEnd || postorderStart > postorderEnd) {
            return nullptr;
        }
        int rootVal = postorder[postorderEnd];
        TreeNode* root = new TreeNode(rootVal);
        int inorderRootIndex = index[rootVal];
        int leftSubtreeSize = inorderRootIndex - inorderStart;
        root->left = buildTreeHelper(inorder, postorder, inorderStart, inorderRootIndex - 1, postorderStart, postorderStart + leftSubtreeSize - 1, index);
        root->right = buildTreeHelper(inorder, postorder, inorderRootIndex + 1, inorderEnd, postorderStart + leftSubtreeSize, postorderEnd - 1, index);
        return root;
    }
};

```
![image](https://github.com/user-attachments/assets/e91523ac-99b6-4e71-a8dd-f91d6674c9f3)

https://leetcode.com/problems/kth-smallest-element-in-a-bst/
```
class Solution {
    private:
        void inorder(TreeNode* root, vector<int>&a){
            if(root==nullptr){
                return;
            }
            
            // traverse left subtree
            inorder(root->left, a);
            // store value of root on which we are standing
            a.push_back(root->val);
            // process the right subtree
            inorder(root->right,a);
        }

public:
    int kthSmallest(TreeNode* root, int k) {
        // creating a vector of int
        vector<int>a;
        //calling inorder traversal
        inorder(root, a);
        //returning the ans..
        return a[k-1];
    }
};
```
![image](https://github.com/user-attachments/assets/21fc7743-5846-466e-ba7d-30693e987d32)

https://leetcode.com/problems/populating-next-right-pointers-in-each-node/
```
 Node* connect(Node* root) {
        if(!root) return nullptr;
        queue<Node*> q;
        q.push(root);        
        while(size(q)) {
            Node* rightNode = nullptr;                    // set rightNode to null initially
            for(int i = size(q); i; i--) {                // traversing each level
                auto cur = q.front(); q.pop();            // pop a node from current level and,
                cur -> next = rightNode;                  // set its next pointer to rightNode
                rightNode = cur;                          // update rightNode as cur for next iteration
                if(cur -> right)                          // if a child exists
                    q.push(cur -> right),                 // IMP: push right first to do right-to-left BFS
                    q.push(cur -> left);                  // then push left
            }
        }
        return root;
    }
```
![image](https://github.com/user-attachments/assets/58a55772-c0ef-469c-934f-f79bbae02245)



