# java_basics

### Compile and Run
```sh
javac hello_world.java
java hello_world
```

### Hello World
```java
public class hello_world {
    public static void main(String args[]){
        System.out.println("Hello Wold");
    }
}
```

### For Loop
```java
public class hello_world {
    public static void main(String args[]){
        for (int i=1;i<=5;i++){
            System.out.println("Hello World "+i);
        }
    }
}
```

### While Loop

```java
public class hello_world {
    public static void main(String args[]){
        int k=1;
        while (k<=5){
            System.out.println("Hello World "+k);
            k++;
        }
    }
}
```

### Conditional Statements
```java
public class hello_world {
    public static void main(String args[]){
        int k=1;

        if (k==1){
            System.out.println("k is equal to 1");
        }
        else if(k==2){
            System.out.println("k is equal to 2");
        }
        else{
            System.out.println("k is not equal to 1 and 2");
        }
    }
}
```


## Binary Tree

1. Preorder - node,left,right
2. Inorder - left,node,right
3. Postorder - left,right,node

```java
public class BinaryTree{

	public TreeNode root;
	
	public class TreeNode {
	    public int data;
	    public TreeNode left;
	    public TreeNode right;
	        
	    public TreeNode(int data) {
	        this.data = data;
	    }
	}
}
```

### Recursive Preorder Traversal

```java
public void preOrder(TreeNode root) {
	if(root == null) { // base case
		return;
	}
	System.out.print(root.data + " ");
	preOrder(root.left);
	preOrder(root.right);
}
```

```java
public class BinaryTree{
    
    public TreeNode root;

    public class TreeNode{
        public int data;
        public TreeNode left;
        public TreeNode right;

        public TreeNode(int data){
            this.data=data;
        }
    }

    public void createBinaryTree(){
        TreeNode first = new TreeNode(4);
        TreeNode second = new TreeNode(5);
        TreeNode third = new TreeNode(6);
        TreeNode fourth = new TreeNode(7);
        TreeNode fifth = new TreeNode(8);

        root=first;
        
        first.left = second;
        first.right = third;

        third.left = fourth;
        third.right = fifth;

    }

    public void preOrderTraversal(TreeNode root){
        if (root == null){
            return;
        }
        System.out.println(root.data);
        preOrderTraversal(root.left);
        preOrderTraversal(root.right);

    }


    public static void main(String[] args){
        BinaryTree bt = new BinaryTree();
        bt.createBinaryTree();
        bt.preOrderTraversal(bt.root);
    }
}

```


### Iterative Preorder Traversal

```java
    public void iterativePreOrder(TreeNode root){
        if (root==null){
            return;
        }
        Stack<TreeNode> stack = new Stack<>();
        stack.push(root);
        while(!stack.isEmpty()){
            TreeNode temp = stack.pop();
            System.out.println(temp.data);
            if (temp.right!=null){
                stack.push(temp.right);
            }
            if (temp.left!=null){
                stack.push(temp.left);
            }
        }
    }
```

```java
import java.util.Stack;

public class BinaryTree{
    
    public TreeNode root;

    public class TreeNode{
        public int data;
        public TreeNode left;
        public TreeNode right;

        public TreeNode(int data){
            this.data=data;
        }
    }

    public void createBinaryTree(){
        TreeNode first = new TreeNode(4);
        TreeNode second = new TreeNode(5);
        TreeNode third = new TreeNode(6);
        TreeNode fourth = new TreeNode(7);
        TreeNode fifth = new TreeNode(8);

        root=first;
        
        first.left = second; //secound(5)<--first(4)-->third(6)
        first.right = third;

        third.left = fourth; //forth(7)<--third(6)-->fifth(8)
        third.right = fifth;

    }

    public void iterativePreOrder(TreeNode root){
        if (root==null){
            return;
        }
        Stack<TreeNode> stack = new Stack<>();
        stack.push(root);
        while(!stack.isEmpty()){
            TreeNode temp = stack.pop();
            System.out.println(temp.data);
            if (temp.right!=null){
                stack.push(temp.right);
            }
            if (temp.left!=null){
                stack.push(temp.left);
            }
        }
    }


    public static void main(String[] args){
        BinaryTree bt = new BinaryTree();
        bt.createBinaryTree();
        bt.iterativePreOrder(bt.root);
    }
}

```


### Recursive Inorder Traversal

- Traverse the left subtree in In order fashion.
- Visit the root node.
- Traverse the right subtree in In order fashion.

```java
public void recursiveInorder(TreeNode root){
	if (root==null){
		return;
	}
	recursiveInorder(root.left);
	System.out.println(root.data+" ");
	recursiveInorder(root.right);
}
```

```java
import java.util.Stack;

public class BinaryTree{
    
    public TreeNode root;

    public class TreeNode{
        public int data;
        public TreeNode left;
        public TreeNode right;

        public TreeNode(int data){
            this.data=data;
        }
    }

    public void createBinaryTree(){
        TreeNode first = new TreeNode(4);
        TreeNode second = new TreeNode(5);
        TreeNode third = new TreeNode(6);
        TreeNode fourth = new TreeNode(7);
        TreeNode fifth = new TreeNode(8);

        root=first;
        
        first.left = second;
        first.right = third;

        third.left = fourth;
        third.right = fifth;

    }

    public void recursiveInorder(TreeNode root){
        if (root==null){
            return;
        }
        recursiveInorder(root.left);
        System.out.println(root.data+" ");
        recursiveInorder(root.right);
    }

    public static void main(String[] args){
        BinaryTree bt = new BinaryTree();
        bt.createBinaryTree();
        bt.recursiveInorder(bt.root);
    }
}

```

### Iterative Inorder Traversal
```java
  public void iterativeInorder(TreeNode root){
        if (root==null){
            return;
        }
        Stack<TreeNode> stack = new Stack<>();
        TreeNode temp = root;
        while(!stack.isEmpty()||temp!=null){
            if(temp!=null){
                stack.push(temp);
                temp = temp.left;
            }
            else{
                temp = stack.pop();
                System.out.println(temp.data+" ");
                temp= temp.right;

            }
        }
        
    }
```

```java
import java.util.Stack;

public class BinaryTree{
    
    public TreeNode root;

    public class TreeNode{
        public int data;
        public TreeNode left;
        public TreeNode right;

        public TreeNode(int data){
            this.data=data;
        }
    }

    public void createBinaryTree(){
        TreeNode first = new TreeNode(4);
        TreeNode second = new TreeNode(5);
        TreeNode third = new TreeNode(6);
        TreeNode fourth = new TreeNode(7);
        TreeNode fifth = new TreeNode(8);

        root=first;
        
        first.left = second;
        first.right = third;

        third.left = fourth;
        third.right = fifth;

    }

    public void iterativeInorder(TreeNode root){
        if (root==null){
            return;
        }
        Stack<TreeNode> stack = new Stack<>();
        TreeNode temp = root;
        while(!stack.isEmpty()||temp!=null){
            if(temp!=null){
                stack.push(temp);
                temp = temp.left;
            }
            else{
                temp = stack.pop();
                System.out.println(temp.data+" ");
                temp= temp.right;

            }
        }
        
    }

    public static void main(String[] args){
        BinaryTree bt = new BinaryTree();
        bt.createBinaryTree();
        bt.iterativeInorder(bt.root);
    }
}
```

### Recursive Postorder Traversal

- Traverse the left subtree in Post order fashion.
- Traverse the right subtree in Post order fashion.
- Visit the node.

```java
    public void recursivePostorder(TreeNode root){
        if (root==null){
            return;
        }
        recursivePostorder(root.left);
        recursivePostorder(root.right);
        System.out.println(root.data+" ");
    }
```
