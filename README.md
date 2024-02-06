# go
```=gp
package main

import (
	"fmt"
)

type NodeType struct {
	Element  string
	Children []NodeType
}

func main() {
	data := map[string][]string{
		"node1": []string{"node2", "node3", "node4", "node5"},
		"node2": []string{"node7"},
		"node5": []string{"node6"},
		"node6": []string{"node8"},
	}

	// Construct the tree from the given data
	rootNode := constructTree(data, "node1")
	fmt.Println(rootNode)
	// Perform BFS traversal
	fmt.Println("BFS Traversal:")
	bfsTraversal(rootNode)

}

func constructTree(data map[string][]string, node string) NodeType {
	children := make([]NodeType, 0)
	for _, child := range data[node] {
		children = append(children, constructTree(data, child))
	}
	return NodeType{Element: node, Children: children}
}

func bfsTraversal(node NodeType) {
	queue := []NodeType{node}
	for len(queue) > 0 {
		current := queue[0]
		queue = queue[1:]
		fmt.Printf("%s: [", current.Element)
		for _, child := range current.Children {
			if len(child.Children) == 0 {
				fmt.Printf(" %s ", child.Element)
			} else {
				fmt.Printf("\n   %s: ", child.Element)
			}
			queue = append(queue, child)
		}
		fmt.Printf("], ")
	}
}

```



```

	originData := []map[string]string{
		{"parent": "node1", "child": "node2"},
		{"parent": "node1", "child": "node3"},
		{"parent": "node1", "child": "node4"},
		{"parent": "node2", "child": "node7"},
		{"parent": "node5", "child": "node6"},
		{"parent": "node6", "child": "node8"},
	}

	data2 := make(map[string][]string)

	for _, item := range originData {
		parent := item["parent"]
		child := item["child"]

		if _, exists := data2[parent]; !exists {
			data2[parent] = make([]string, 0)
		}
		data2[parent] = append(data2[parent], child)
	}
	fmt.Println()
	fmt.Println(data2)
```
