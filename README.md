class Solution {
public:
    map<int, vector<int>> mp;
    int result=0;
    map<int, bool>visited;
    void dfs(TreeNode* root) {
        if (root == NULL)
            return;
            visited[root->val]=false;
        if (root->left) {
            mp[root->left->val].push_back(root->val);
            mp[root->val].push_back(root->left->val);
            dfs(root->left);
        }
        if (root->right) {
            mp[root->right->val].push_back(root->val);
            mp[root->val].push_back(root->right->val);
            dfs(root->right);
        }
        return;
    }

    int amountOfTime(TreeNode* root, int start) { 
        dfs(root); 
        
        queue<pair<int, int>>que;
        que.push({start, 0});
        visited[start]=true;
        while(!que.empty()){
            pair<int, int>pr=que.front();

            que.pop();
            int currNode=pr.first, time=pr.second;
            visited[currNode]=true;
            result=max(result, time);
            for(auto n:mp[currNode]){
                if(visited[n]==false) que.push({n, time+1});
            }

        }
        return result;
    }
};
