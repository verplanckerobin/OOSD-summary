# OOSD Summary
## Hoofdstuk 1 Overerving
primitieve var -> waarde  
referentie var -> instantie (klasse, array)  
referentie var -> null (leeg, niets)  

SUBKLASSE -> extends (java code)  
Check of subklasse is -> instanceof (java code)  

OPERATOR "==" vergelijkt waarden, primitief of adressen in geheugen van referentievariabelen  
METHODE equals vergelijkt op basis van inhoud  
--> indien niet overschreven: overerven van Object Klasse  
--> overschrijven is zelf bepalen waarop vergeleken wordt = source - Generate hashCode() and equals()

Let op constructor in subklasses! Moet constructor van SUPERklasse aanroepen

Methode binnen subklasse overschrijven --> @override (java code)  
--> methode van superklasse aanroepen binnen subklasse --> super. (java code)

**Abstracte klasse** = kan geen instanties maken van deze klasse  
--> (*cursief in UML*)  
--> public abstract class (java code)  
**Abstracte methode** = methode zonder implementatie, enkel signatuur  
--> (*cursief in UML*)  
--> public abstract Type naam(); (java code, let op ; en geen {})  

Attribuut **static**: er bestaat slechts 1 instantie van attribuut = klassevariabele  
--> wordt gedeeld over alle instanties, ongeacht aantal  
--> onderlijnt in UML  
--> om methode te gebruiken moet EERST een object aangemaakt worden

Keyword **final**
- Attribuut: 
  - final klassevariabele: waarde toekennen bij declaratie
  - final instantievariabele: waarde toekennen binnen constructor
- Variabele: lokaal in methode, eenmalig waarde toegekend
- Methode: vb setter, voorkomen dat methode kan overschreven worden in subklasse

## Hoofdstuk 2 Polymorfisme & Interfaces
Polymorfisme = veelvormigheid, komt voort uit de 'IS EEN' relatie  
Vb: Rechthoek erft van Veelhoek erft van Figuur  
--> Rechthoek r1 = new Rechthoek();  
--> Rechthoek r2 = new Veelhoek(); (een rechthoek is ook een veelhoek, polymorfisme)
 

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
