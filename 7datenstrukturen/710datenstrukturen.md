### Sie können eine einfache Liste selber implementieren

---

[Zurück](700datenstrukturen.md)

#### Node für Strings

```java
package list;

public class Node {
	
	private String data;
	private Node next;
	
	public Node(Node n, String d) {
		next = n;
		data = d;
	}
	
	public void setData(String d) {
		data = d;
	}
	
	public String getData() {
		return data;
	}
	
	public void setNext(Node n) {
		next = n;
	}
	
	public Node getNext() {
		return next;
	}
	
}
```

#### List mit obigen Nodes

```java
package list;

public class List {
	
	private Node head;
	
	public List() {
		head = null;
	}
	
	public boolean isEmpty() {
		return (head == null);
	}
	
	public void insert(String d) {
		head = new Node(head, d);
	}
	
	public boolean isFound(String d) {
		Node actualNode = head;
		while((actualNode != null) && !d.equals(actualNode.getData())) {
			actualNode = actualNode.getNext();
		}
		if(actualNode == null) {
			return false;
		}
		else {
			return true;
		}
	}
	
	public void remove(String d) {
		Node actualNode = head;
		Node previousNode = null;
		while((actualNode != null) && !d.equals(actualNode.getData())) {
			previousNode = actualNode;
			actualNode = previousNode.getNext();
		}
		if(actualNode != null) {
			if(actualNode == head) {
				head = actualNode.getNext();
			}
			else {
				previousNode.setNext(actualNode.getNext());
			}
		}
	}
	
	public void print() {
		Node actualNode = head;
		while(actualNode != null) {
			System.out.println(actualNode.getData());
			actualNode = actualNode.getNext();
		}
	}
	
}
```

#### Verwendung

```java
package list;

public class Main {
	
	public static void main(String[] args) {
		
		String[] names = new String[]{"Richard", "Torvalds", "Babbage"};
		
		List users = new List();
		
		for(String i : names) {
			users.insert(i);
		}
		
		users.print();
		
	}
	
}
```

---
Siehe DAT1 S.23-28
