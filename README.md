# OOSD Conversions
## String to Int
```
String s = "1";
int i = Integer.parseInt(s);
```
## Int to String
```
int i = 10;
String s = String.valueOf(i);
```
## String to char
```
String s = "hello";
char c = s.charAt(0); //returns "h"
```
## char to String
```
char c = 's';
String s = String.valueOf(c);
```
## Array to List
```
String[] colors = {"Black","Blue","Red"}; //array
LinkedList<String> lijst = new LinkedList<>(Arrays.asList(colors)); //list
```
## List to Array
Zie hierboven
```
lijst.add("Pink")
colors = lijst.toArray(new String[lijst.size()]);
```

# Collections
## Methode voor afdrukken van lijst
```
private void printList(Collection<String> collection) {
  //1. met enhanced for
  for (String color : collection)
    System.out.printf("%s ", color);
      
  // 2. met iterator
  Iterator<String> iterator = collection.iterator();
  while (iterator.hasNext())
    System.out.printf("%s ", iterator.next());
}
```
## Methode voor verwijderen elementen uit Collection
```
private void removeItems(Collection<String> col1, Collection<String> col2) {
  col1.removeAll(col2);
}
```
# List
## Methode voor verwijderen elementen uit List
```
private void removeItems(List<String> list, int start, int eind) {
  list.subList(start, end).clear();
}
```
## Methode om List reversed weer te geven
```
private void printReverse(List<String> list) {
  ListIterator<String> iterator = list.listIterator(list.size()); //we beginnen achteraan
  while(iterator.hasPrevious())
    System.out.printf("%s ", iterator.previous());
}
```
## Methode omzetten naar hoofdletters in List
```
private void convertToUpperCase(List<String> list) {
  ListIterator<String> iterator = list.listIterator(); //vooraan
  while(iterator.hasNext())
    String s = iterator.next(); //get item
    iterator.set(s.toUpperCase());
}
```
