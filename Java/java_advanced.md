## Loop Detection
### Floyd’s Detection

```java
public class LinkedList{

	public class Node{
	int data;
	Node next;
	Node(int data){
		this.data = data;
		next=null;
	}
}

Node head;

public void push(int newData){
	Node newNode = new Node(newData);
	newNode.next = head;
	head = newNode;
}

public void detectLoop(){
	Node slow = head;
	Node fast = head;

	while(slow!=null && fast!=null && fast.next!=null){
		slow=slow.next;
		fast=fast.next.next;

		if(slow==fast){
			System.out.println("Loop Detected");
			return;
		}
	}
	System.out.println("Loop not Detected");
}

public static void main(String args[]){
	LinkedList l1 = new LinkedList();
	l1.push(1);
	l1.push(2);
	l1.push(3);
	l1.push(4);
	l1.push(5);

	l1.head.next.next = l1.head; // Making it looped
	l1.detectLoop();
}
}
```

### Hash-set Method
```java
import java.util.HashSet;

public class LinkedListHashSet {
    public class Node{
        int data;
        Node next;

        Node(int data){
            this.data = data;
        }
    }

    Node head;

    public void push(int newData){
        Node newNode = new Node(newData);
        newNode.next = head;
        head = newNode;
    }

    public void detectLoopHash(Node h){
        HashSet<Node> s = new HashSet<Node>();
        while(h!=null){
            if(s.contains(h)){
                System.out.println("Loop Detected");
                return;
            }
            s.add(h);
            h = h.next;
        }     
        System.out.println("Loop Not Detected");
        return;
    }

    public static void main(String args[]){
        LinkedListHashSet l1 = new LinkedListHashSet();
        l1.push(1);
        l1.push(2);
        l1.push(3);
        l1.push(4);
        l1.push(5);
        l1.head.next.next.next = l1.head;

        l1.detectLoopHash(l1.head);


    }
}

```
## Recover BST
```java
import java.util.*;

// Definition for a binary tree node.
class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;
    TreeNode(int x) { val = x; }
}

public class RecoverBST {
    
    TreeNode firstNode = null;
    TreeNode secondNode = null;
    TreeNode prevNode = new TreeNode(Integer.MIN_VALUE); // Initializing prevNode with minimum possible value
    
    public void recoverTree(TreeNode root) {
        // Traverse the tree to find the swapped nodes
        inorderTraversal(root);
        
        // Swap the values of the two nodes
        int temp = firstNode.val;
        firstNode.val = secondNode.val;
        secondNode.val = temp;
    }
    
    private void inorderTraversal(TreeNode node) {
        if (node == null) return;
        
        inorderTraversal(node.left);
        
        // Check for the swapped nodes
        if (firstNode == null && prevNode.val >= node.val) {
            firstNode = prevNode;
        }
        if (firstNode != null && prevNode.val >= node.val) {
            secondNode = node;
        }
        prevNode = node;
        
        inorderTraversal(node.right);
    }

    public static void main(String[] args) {
        RecoverBST solution = new RecoverBST();
        Scanner scanner = new Scanner(System.in);

        // Input number of nodes
        System.out.print("Enter the number of nodes: ");
        int n = scanner.nextInt();

        // Input the values of nodes in in-order traversal order (-1 for null):
        System.out.println("Enter the values of nodes in in-order traversal order (-1 for null):");
        TreeNode root = constructBinaryTree(scanner, n);

        // Recover the BST
        solution.recoverTree(root);

        // Output the recovered BST
        System.out.println("Recovered BST:");
        inorderTraversalPrint(root);
    }

    // Helper method to construct binary tree
    private static TreeNode constructBinaryTree(Scanner scanner, int n) {
        TreeNode[] nodes = new TreeNode[n];
        for (int i = 0; i < n; i++) {
            int value = scanner.nextInt();
            if (value != -1) { // Check if the input value is not null
                nodes[i] = new TreeNode(value);
            } else {
                nodes[i] = null; // Mark as null
            }
        }

        for (int i = 0; i < n; i++) {
            if (nodes[i] != null) {
                if (2 * i + 1 < n) {
                    nodes[i].left = nodes[2 * i + 1];
                }
                if (2 * i + 2 < n) {
                    nodes[i].right = nodes[2 * i + 2];
                }
            }
        }

        return nodes[0];
    }
    
    // Helper method for printing tree using inorder traversal
    private static void inorderTraversalPrint(TreeNode node) {
        if (node == null) return;
        
        inorderTraversalPrint(node.left);
        System.out.print(node.val + " ");
        inorderTraversalPrint(node.right);
    }
}

```

## Vertical Order Traversal

```java
import java.util.*;

// Definition for a binary tree node.
class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;
    TreeNode(int x) { val = x; }
}

public class VerticalOrderTraversal {
    
    // Helper class to store node and its horizontal distance
    class NodeHD {
        TreeNode node;
        int hd;
        NodeHD(TreeNode node, int hd) {
            this.node = node;
            this.hd = hd;
        }
    }
    
    public List<List<Integer>> verticalOrder(TreeNode root) {
        List<List<Integer>> result = new ArrayList<>();
        if (root == null) return result;
        
        // TreeMap to store nodes at different horizontal distances
        TreeMap<Integer, List<Integer>> map = new TreeMap<>();
        
        // Queue for level order traversal
        Queue<NodeHD> queue = new LinkedList<>();
        queue.offer(new NodeHD(root, 0)); // root has horizontal distance 0
        
        while (!queue.isEmpty()) {
            NodeHD nodeHD = queue.poll();
            TreeNode node = nodeHD.node;
            int hd = nodeHD.hd;
            
            // Put the current node into the map based on its horizontal distance
            if (!map.containsKey(hd))
                map.put(hd, new ArrayList<>());
            map.get(hd).add(node.val);
            
            // Enqueue left and right children with updated horizontal distances
            if (node.left != null)
                queue.offer(new NodeHD(node.left, hd - 1));
            if (node.right != null)
                queue.offer(new NodeHD(node.right, hd + 1));
        }
        
        // Extract values from the TreeMap and add to result list
        for (List<Integer> list : map.values()) {
            result.add(list);
        }
        
        return result;
    }

    public static void main(String[] args) {
        VerticalOrderTraversal solution = new VerticalOrderTraversal();
        Scanner scanner = new Scanner(System.in);

        // Input number of nodes
        System.out.print("Enter the number of nodes: ");
        int n = scanner.nextInt();

        // Input the values of nodes in level order
        System.out.println("Enter the values of nodes in level order (-1 for null):");
        TreeNode root = constructBinaryTree(scanner, n);

        // Perform vertical order traversal
        List<List<Integer>> verticalOrderTraversal = solution.verticalOrder(root);

        // Output the vertical order traversal
        System.out.println("Vertical Order Traversal:");
        for (List<Integer> list : verticalOrderTraversal) {
            System.out.println(list);
        }
    }

    // Helper method to construct binary tree
    private static TreeNode constructBinaryTree(Scanner scanner, int n) {
        TreeNode[] nodes = new TreeNode[n];
        for (int i = 0; i < n; i++) {
            int value = scanner.nextInt();
            if (value != -1) { // Check if the input value is not null
                nodes[i] = new TreeNode(value);
            } else {
                nodes[i] = null; // Mark as null
            }
        }

        TreeNode root = nodes[0];
        for (int i = 0; i < n; i++) {
            if (nodes[i] != null) {
                if (2 * i + 1 < n) {
                    nodes[i].left = nodes[2 * i + 1];
                }
                if (2 * i + 2 < n) {
                    nodes[i].right = nodes[2 * i + 2];
                }
            }
        }

        return root;
    }
}
```

## Boundary Order Traversal

```java
import java.util.*;

// Definition for a binary tree node.
class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;
    TreeNode(int x) { val = x; }
}

public class BoundaryTraversal {
    
    public List<Integer> boundaryOfBinaryTree(TreeNode root) {
        List<Integer> boundary = new ArrayList<>();
        if (root == null) return boundary;
        
        boundary.add(root.val);
        leftBoundary(root.left, boundary);
        leaves(root.left, boundary);
        leaves(root.right, boundary);
        rightBoundary(root.right, boundary);
        
        return boundary;
    }
    
    private void leftBoundary(TreeNode node, List<Integer> boundary) {
        if (node == null || (node.left == null && node.right == null)) return;
        
        boundary.add(node.val);
        if (node.left != null)
            leftBoundary(node.left, boundary);
        else
            leftBoundary(node.right, boundary);
    }
    
    private void rightBoundary(TreeNode node, List<Integer> boundary) {
        if (node == null || (node.left == null && node.right == null)) return;
        
        if (node.right != null)
            rightBoundary(node.right, boundary);
        else
            rightBoundary(node.left, boundary);
        boundary.add(node.val);
    }
    
    private void leaves(TreeNode node, List<Integer> boundary) {
        if (node == null) return;
        
        if (node.left == null && node.right == null)
            boundary.add(node.val);
        
        leaves(node.left, boundary);
        leaves(node.right, boundary);
    }

    public static void main(String[] args) {
        BoundaryTraversal solution = new BoundaryTraversal();
        Scanner scanner = new Scanner(System.in);

        // Input number of nodes
        System.out.print("Enter the number of nodes: ");
        int n = scanner.nextInt();

        // Input the values of nodes in pre-order traversal order (-1 for null):
        System.out.println("Enter the values of nodes in pre-order traversal order (-1 for null):");
        TreeNode root = constructBinaryTree(scanner, n);

        // Get the boundary traversal
        List<Integer> boundaryTraversal = solution.boundaryOfBinaryTree(root);

        // Output the boundary traversal
        System.out.println("Boundary Traversal:");
        for (int val : boundaryTraversal) {
            System.out.print(val + " ");
        }
    }

    // Helper method to construct binary tree
    private static TreeNode constructBinaryTree(Scanner scanner, int n) {
        TreeNode[] nodes = new TreeNode[n];
        for (int i = 0; i < n; i++) {
            int value = scanner.nextInt();
            if (value != -1) { // Check if the input value is not null
                nodes[i] = new TreeNode(value);
            } else {
                nodes[i] = null; // Mark as null
            }
        }

        for (int i = 0; i < n; i++) {
            if (nodes[i] != null) {
                if (2 * i + 1 < n) {
                    nodes[i].left = nodes[2 * i + 1];
                }
                if (2 * i + 2 < n) {
                    nodes[i].right = nodes[2 * i + 2];
                }
            }
        }

        return nodes[0];
    }
}

```