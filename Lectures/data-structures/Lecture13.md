## Binary Tree

In computer science, a binary tree is a tree data structure in which each node has at most two children, which are referred to as the left child and the right child.
### Essentials about Binary Tree

* **Binary Tree:** Each element in the Tree Has at most a left and right child.
* **Applications:** Usually used when we store information that naturally forms a hierarchy or when we need to execute fast search operation.
* **Size**: Number of nodes in the Binary Tree. 



### Struct of a node
```
struct node
{
    int data;
    struct node *left;
    struct node *right; 
}
```

### Check if an element exists

Before insert a new node in the BT, we need to be sure that the same element is not already stored, so we need the following function:

```
bool does_element_exists(struct node *root , int target)
{
    // BT is empty, no element to search
    if(root == NULL)
        return false;
    else
    {
        if(root->data == x) return true; 
        else if(x < node->data)
            return does_element_exists(root->left, x);
        return does_element_exists(root->right, x);
    }
}
```

### Create new node
```
struct node *NewNode(int data)
{
    struct node *root = new(struct node);
    node->data = data;
    node->left = node->right = NULL;
}
```

### Insert

Rember that in BT is not allowed to have duplicate elements, for this reason for every insert operation, we need to check first if element exists using the [exists checker function](#Check-if-an-element-exists) and the [create node function](#Create-new-node)




### Traversal
A traversal is a process that visits all the nodes in the tree. Since a tree is a nonlinear data structure, there is no unique traversal. We will consider several traversal algorithms with we group in the following two kinds:

* depth-first traversal
* breadth-first traversal


There are Three types of depth -First-Traversals:

1. Inorder (Left, Root, Right) : 4 2 5 1 3
```
void inorder(struct Node *root)
{
    if(root == NULL)
        return; 
    search(root->left);
    cout <<root->data << " ";
    search(root->right);
}
```
2. Preorder (Root, Left, Right) : 1 2 4 5 3
```
void preoder(struct Node *root)
{
    if(root == NULL)
        return; 
    cout <<root->data << " ";
    search(root->left);
    search(root->right);
}

```
3. Postorder (Left, Right, Root) : 4 5 2 3 1
void inorder(struct Node *root)
{
    if(root == NULL)
        return; 
    search(root->left);
    search(root->right);
    cout <<root->data << " ";
}

There is only one kind of breadth-first-traversal, the Breadth First or Level Order Traversal : 1 2 3 4 5

### Height vs Depth

During my first approach to Tree, I swapped the meaning of Height and Depth. 

![Depth vs Height BT](../../images/tree-depth.png)
###### Source: Stackoverflow, the bible

### Max Depth

The max depth is the number of nodes along the longhest path from the root node down to the farthest leaf(external) node.

```
int maxDepth(struct node *root)
{
    if(root == NULL)
        return 0; 
    else
    {
        unsigned long int leftDepth = maxDeth(node->left);
        unsigned long int rightDepth = maxDepth(node->right);

        // Return the biggest counter
        if(leftDepth > rightDepth)
            return leftDepth+1;
        else    
            return rightDepth+1;
    }
}
```

* [Extra information: Tutorial 1](https://www.cs.cmu.edu/~adamchik/15-121/lectures/Trees/trees.html)
* [Extra information: Tutorial 2](http://cslibrary.stanford.edu/110/BinaryTrees.html)

## Print node at k distance from  root 

```
void print_level_k(node *root, int k)
{
    if(root == NULL)
        return;
    if( k == 0)
    {
        cout <<root->data<<endl;
        return;
    }
    else
    {
        print_level_k(root->left, k-1);
        print_level_k(root->right, k-1);
    }
}

```

## Height of a tree
int height(node *root)
{
    if(height == NULL)
        return 0; 
    else
    {
     /* compute the height of each subtree */
        int lHeight = height(node->left);  
        int rHeight = height(node->right);  
        /* use the larger one */
          
        return (lHeight > rHeight)? (lHeight + 1): (rHeight + 1);    
    }
}

## Count Leaves in a Binary Tree

* **Leaves:**

## Diameter of a Binary Tree

Diameter (also width): number of nodes on thelongest path between two end nodes.
The diameter of a tree T is the largest of the following quantities:
* The diameter of the left subtreee
* Diameter of right subtree
* Longest path between leaves that goes thourhg the root T (computed from the height of  a tree).
![Diameter-of-tree](../../images/diameter_of_tree.png)
```
int height(Node *head)
{
    if(head == NULL)
        return 0;
    return 1 + max(height(node->left), height(node->right))
}
```
```
int diameter(Node *head)
{
    if(head == NULL)
        return 0;
    else
    {
        left_height = height(root->left);
        right_height = height(root->right);

        // Get the diameter of left and right sub-trees
        left_diameter = diameter(root->left);
        right_diameter = diameter(root->right)

        return max(left_height + right_height +1, max(left_diameter, right_diameter));
    }
}
```
###### Image by Geeks for Geeks

## Left or Right view of Binary Tree


![Left View](../../media/left_view.png)
###### Left view, images: Geeks for Geeks
## Check if a tree is balanced

## Ancestors 
* [Print Ancestors of a given node](https://www.geeksforgeeks.org/print-ancestors-of-a-given-node-in-binary-tree/)
* [Lowest common Ancestor of a given binary tree](https://www.geeksforgeeks.org/print-ancestors-of-a-given-node-in-binary-tree/)

## Binary Tree (BT), convert it to a Doubly Linked List(DLL) In-Place.
Recursively look for the node with no grandchildren and both left and right child in the left sub-tree. Then store node->right in temp and make node->right=node->left. Insert temp in first node NULL on right of node by node=node->right. Repeat until it is converted to linked list.

Flatten operation: convert from BT to Linked list
Inorder printing of the BT allws to have the flatted BT elements in increasing order

```
void flatten(Node * root)
{
    if(root == NULL || root->left == NULL && root->right == NULL)
        return; 
    if(root->left != NULL)
    {
        //Move the left subtree in the right subtree
        if(root->left != NULL)
        {
            flatten(root->left);

            Node * tempraryRight = root->right;
            root->right = root->left;
            root->left = NULL;

            // Find the position to insert the new node
            Node *t = root->right; 
            while(t->right != NULL)
                t = t->right;
        
            // Insert the value
            t->right = temporaryRight;
        }
        // Call the same function for root->ight
        flatten(root->right);

    }
}
```
## Vertical traversal of Binary Tree
Traverse a Binary Tree vertically means ge the minimum and maximum horizontal distance with respect to root. 
![Vertical Print](../../media/vertical_bt.png)
###### Image provided by Geeks For Geeks
```
// min: min horizonal distance from root
// max: max horizonal distance from root
//  horizontal_distnace: horizonal distance of current from node from root
void findMinMax(Node *root, *min, *max, horizontal_distance)
{
    if(root == NULL)
        return;
    if(horizontal_distance < min) *min = horizontal_distance;
    else if( horizontal_distance > max) *max = horizontal_distance;

    findMinMax(root ->left, min, max, horizontal_distance-1);
    findMinMax(root -> right, min, max, horizontal_distance+1);
}

void printVerticalLine(Nod * root, line_number, horizontal_distance)
{
    if(root == NULL)
        return; 
    if(horizontal_distance == line_numnber)
        cout << root -> data; <<endl;
    printVerticalLine(root->left, line_number, horizontal_distance-1);
    printVerticalLine(root->right, line_number, horizontal_distance+1);
}
// The main function that prints a given binary tree in 
// vertical order
void verticalOrder(Node *root)
{
    // Get min and max distance respect to the root
    int min = 0,  max =0;
    findMinMax(root, &min, &max, 0);

    /* Iterate all possible vertical lines starting from the leftmost and print
     line by line */
     for(int line_number = min, line_number <= max; line_number++)
     {
         printVerticalLine(root, line_number, 0);
         cout <<endl;
     }
}

```

[Find distance between root and a given node](https://www.youtube.com/watch?v=pavbfn1FHrs&feature=emb_rel_end)

## Practice with Binary Tree

Perfect, above you have find all the definition that you will need to know before to solve the following exercises. 
* Get the Height of a Binary Tree
* Minimum elment in BST
* Clone a Binary Tree
* Size of a Binary Tree
* Inorder, postorder, preorder traversal
* Maximum Node Level
* Remove Heal Nodes
* K distance from root
* Sum of Binary Tree
* Sum of Leaf Nodes
* Sum of right Leaf Nodes
* Count Non-leaf Nodes
* Minimum Depth of a Binary Tree
* Make a Binary Tree from Linked List
* Determine if two Trees are identical
* Perfect Binary Tree
* Vertical Sum

[More exercises](https://practice.geeksforgeeks.org/explore/?category%5B%5D=Tree&page=1)
