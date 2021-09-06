// FirstRepository
// This is my first repository to understand github.

#include <bits/stdc++.h>
using namespace std;

//______________________________________C:\Users\Aman Joshi\AppData\Roaming\Sublime Text 3\Packages\User_____________________________________________________________________
// Driver program

struct Node
{
    int data;
    Node *left, *right;

    Node() {

        left = NULL;
        right = NULL;
    }
    Node(int x) {

        data = x;
        left = NULL;
        right = NULL;
    }
};


Node *insert( int arr[], int n) {

    if (arr[0] == -1)
        return NULL;
    Node *root = new Node(arr[0]);

    queue<Node*> q;
    int i = 1;
    q.push(root);

    while (!q.empty() && i < n) {

        Node *curr = q.front();
        q.pop();

        if (arr[i] != -1) {

            curr->left = new Node(arr[i]);
            q.push(curr->left);


        }
        else curr->left = NULL;
        i++;

        if (arr[i] != -1) {

            curr->right = new Node(arr[i]);
            q.push(curr->right);

        }
        else curr->right = NULL;
        i++;
    }

    return root;

}

void printInorder(Node *root) {

    if (root == NULL)
        return;

    printInorder(root->left);
    cout << root->data << " ";
    printInorder(root->right);
}
void helper(Node *root, Node **front, Node **end) {

    if (root == NULL)
        return;

    helper(root->left, front, end);

    Node *temp = new Node(root->data);

    if (*front == NULL) {

        *front = temp;
        *end = temp;
    }

    else {

        (*end)->right = temp;
        temp->left = *end;
        *end = (*end)->right;
    }

    helper(root->right, front, end);
}

Node * bToDLL(Node *root)
{
    // your code here
    Node *front = NULL;
    Node *end = NULL;
    helper(root, &front, &end);

    return front;

}


//TO print Dll
void printLL(Node *head) {


    Node *temp = head;
    while (temp->right != NULL) {

        cout << temp->data << " ";
        temp = temp->right;
    }

    cout << temp->data << endl;

    while (temp->left != NULL) {

        cout << temp->data << " ";
        temp = temp->left;
    }

    cout << temp->data << endl;
}
int main()
{
// #ifndef ONLINE_JUDGE
//     freopen("input.txt", "r", stdin);
//     freopen("output.txt", "w", stdout);
// #endif


    int arr[11] = {1, 2, 3, 4, 5, -1, -1, -1, -1, -1, 6};

    int n = sizeof(arr) / sizeof(arr[0]);

    Node *root = insert(arr, n);

    printInorder(root);
    cout << endl;

    Node *head = bToDLL(root);
    printLL(head);
}

// 4 2 5 0 6 0 1 3
// 3 1 0 6 0 5 2 4
