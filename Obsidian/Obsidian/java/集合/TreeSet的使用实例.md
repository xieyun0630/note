# TreeSet的使用实例:创建了Item对象的两个树集。
+ 实例目标：创建Item对象的两个树集。第一个按照部件编号排序，这是Item对象的默认排序顺序。第二个通过使用一个定制的比较器按照描述信息排序。
```java
package treeSet;

import java.util.*;
public class TreeSetTest
{
	 public static void main(String[] args)
	 {
			var parts = new TreeSet<Item>();
			parts.add(new Item("Toaster", 1234));
			parts.add(new Item("Widget", 4562));
			parts.add(new Item("Modem", 9912));
			System.out.println(parts);

			var sortByDescription = new TreeSet<Item>(Comparator.comparing(Item::getDescription));

			sortByDescription.addAll(parts);
			System.out.println(sortByDescription);
	 }
}
```
+ Item类
```java
		package treeSet;

		import java.util.*;
		public class Item implements Comparable<Item>
		{
			 private String description;
			 private int partNumber;

			 /**
				* Constructs an item.
				* @param aDescription the item's description
				* @param aPartNumber the item's part number
				*/
			 public Item(String aDescription, int aPartNumber)
			 {
					description = aDescription;
					partNumber = aPartNumber;
			 }

			 /**
				* Gets the description of this item.
				* @return the description
				*/
			 public String getDescription()
			 {
					return description;
			 }

			 public String toString()
			 {
					return "[description=" + description + ", partNumber=" + partNumber + "]";
			 }

			 public boolean equals(Object otherObject)
			 {
					if (this == otherObject) return true;
					if (otherObject == null) return false;
					if (getClass() != otherObject.getClass()) return false;
					var other = (Item) otherObject;
					return Objects.equals(description, other.description) && partNumber == other.partNumber;
			 }

			 public int hashCode()
			 {
					return Objects.hash(description, partNumber);
			 }

			 public int compareTo(Item other)
			 {
					int diff = Integer.compare(partNumber, other.partNumber);
					return diff != 0 ? diff : description.compareTo(other.description);
			 }
		}
```
[[TreeSet类概念]]