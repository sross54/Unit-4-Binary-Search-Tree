# Unit-4-Binary-Search-Tree
"""
=========================================================
UNIT 4 DISCUSSION: BINARY SEARCH TREES (BST)
=========================================================

INSTRUCTIONS:
This assignment focuses on understanding and implementing a
Binary Search Tree (BST).

You will complete and modify the provided code while explaining
key concepts in your own words using comments and output.
"""


class Node:
    def __init__(self, value):
        # TODO (Student):
        # Store the node's value and initialize references
        # to the left and right child nodes.

        self.value = value
        self.left = None
        self.right = None


class BST:
    def __init__(self):
        # TODO (Student):
        # Initialize an empty Binary Search Tree.

        self.root = None

    def insert(self, value):
        """
        TODO (Student):
        Insert a value into the BST.

        Requirements:
        - Use the recursive helper method.
        - Add comments explaining why insertion depends on
          whether a value is smaller or larger than the
          current node.
        """
        # The first value inserted becomes the root node.
        if self.root is None:
            self.root = Node(value)
        else:
            self.root = self._insert_recursive(self.root, value)

    def _insert_recursive(self, node, value):
        """
        TODO (Student):
        Implement recursive BST insertion.

        Requirements:
        - Create a new node when a position is found.
        - Insert smaller values into the left subtree.
        - Insert larger values into the right subtree.
        - Return the updated node reference.
        """
        # If we reach an empty location, create a new node.
        if node is None:
            return Node(value)

        # In a BST, values smaller than the current node
        # belong in the left subtree.
        if value < node.value:
            node.left = self._insert_recursive(node.left, value)

        # Values larger than the current node belong
        # in the right subtree.
        elif value > node.value:
            node.right = self._insert_recursive(node.right, value)

        # Duplicate values are ignored in this implementation.
        return node

    def search(self, value):
        """
        TODO (Student):
        Search for a value in the BST.

        Requirements:
        - Return True if found.
        - Return False if not found.
        - Add comments explaining why BST search is often
          more efficient than linear search.
        """
        # A BST search is efficient because each comparison
        # eliminates roughly half of the remaining search space.
        # Instead of checking every value, we move directly
        # left or right based on the comparison result.
        return self._search_recursive(self.root, value)

    def _search_recursive(self, node, value):
        """
        TODO (Student):
        Implement recursive BST search.
        """
        if node is None:
            return False

        if value == node.value:
            return True

        if value < node.value:
            return self._search_recursive(node.left, value)

        return self._search_recursive(node.right, value)

    def inorder(self):
        """
        TODO (Student):
        Return a list containing the values from an
        in-order traversal.
        """

        values = []
        self._inorder_recursive(self.root, values)
        return values

    def _inorder_recursive(self, node, values):
        """
        TODO (Student):
        Implement in-order traversal.

        Requirements:
        - Visit the left subtree.
        - Visit the current node.
        - Visit the right subtree.
        - Add comments explaining why this traversal
          produces sorted output in a BST.
        """
        if node is not None:
            # For a BST, smaller values are always stored
            # in the left subtree and larger values are
            # always stored in the right subtree.
            # Visiting Left -> Root -> Right naturally
            # produces output in ascending order.

            self._inorder_recursive(node.left, values)
            values.append(node.value)
            self._inorder_recursive(node.right, values)


def main():
    print("=== UNIT 4: BINARY SEARCH TREES ===")

    # ===============================
    # TODO (Student): BUILD A TREE
    # ===============================
    #
    # Requirements:
    # 1. Create a BST object.
    # 2. Insert at least 7 values.
    # 3. Include values that go into both left
    #    and right subtrees.
    # 4. Display the values inserted.
    # 5. Use comments to explain why a BST is efficient at reducing search space for each step.

    bst = BST()

    values = [50, 30, 70, 20, 40, 60, 80]

    # Each insertion places the value in a specific
    # location based on comparisons, helping maintain
    # the BST structure and enabling faster searches.
    for value in values:
        bst.insert(value)

    print("\n=== TREE CONSTRUCTION ===")
    print("Values inserted:", values)

    # ===============================
    # TODO (Student): IN-ORDER TRAVERSAL
    # ===============================
    #
    # Requirements:
    # 1. Perform an in-order traversal.
    # 2. Display the traversal results.
    # 3. Use comments to explain why the traversal produces
    #    sorted output in a BST.

    print("\n=== IN-ORDER TRAVERSAL ===")

    traversal = bst.inorder()

    # Because BST nodes are ordered by value,
    # an in-order traversal visits values from
    # smallest to largest.
    print("Sorted values:", traversal)

    # ===============================
    # TODO (Student): SEARCH TESTS
    # ===============================
    #
    # Requirements:
    # 1. Search for at least two values that exist.
    # 2. Search for at least two values that do not exist.
    # 3. Use comments to clearly explain the results.

    print("\n=== SEARCH TESTS ===")

    existing_values = [40, 80]
    missing_values = [25, 100]

    for value in existing_values:
        print(f"Search {value}: {bst.search(value)}")

    for value in missing_values:
        print(f"Search {value}: {bst.search(value)}")
    

    # ===============================
    # TODO (Student): EDGE CASES
    # ===============================
    #
    # Demonstrate at least one edge case.
    #
    # Example ideas:
    # - Traverse an empty tree
    # - Search an empty tree
    # - Insert duplicate values
    # - Create a tree with only one node
    #
    # Use comments to explain what happens and why.

    print("\n=== EDGE CASES ===")

    empty_tree = BST()

    # Searching an empty tree immediately returns False
    # because there are no nodes to examine.
    print("Search empty tree for 10:", empty_tree.search(10))

    # Traversing an empty tree returns an empty list.
    print("In-order traversal of empty tree:", empty_tree.inorder())

    # Demonstrating duplicate insertion.
    bst.insert(50)

    # Since duplicates are ignored, the traversal
    # remains unchanged.
    print("After attempting duplicate insert of 50:")
    print(bst.inorder())



if __name__ == "__main__":
    main()
