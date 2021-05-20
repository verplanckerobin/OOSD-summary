# OOSD Summary
## Hoofdstuk 1 Overerving
primitieve var -> waarde  
referentie var -> instantie (klasse, array)  
referentie var -> null (leeg, niets)  

SUBKLASSE -> ```extends```   
Check of subklasse is -> ```instanceof```  

OPERATOR "==" vergelijkt waarden, primitief of adressen in geheugen van referentievariabelen  
METHODE equals vergelijkt op basis van inhoud  
--> indien niet overschreven: overerven van Object Klasse  
--> overschrijven is zelf bepalen waarop vergeleken wordt = source - Generate hashCode() and equals()

Let op constructor in subklasses! Moet constructor van SUPERklasse aanroepen

Methode binnen subklasse overschrijven --> ```@override```   
--> methode van superklasse aanroepen binnen subklasse --> ```super.``` 

**Abstracte klasse** = kan geen instanties maken van deze klasse  
--> (*cursief in UML*)  
--> ```public abstract class``` 
**Abstracte methode** = methode zonder implementatie, enkel signatuur  
--> (*cursief in UML*)  
--> ```public abstract Type naam();``` (let op ; en geen {})  

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
**Polymorfisme** = veelvormigheid, komt voort uit de 'IS EEN' relatie  
- Upcasting
- Downcasting
![image](https://user-images.githubusercontent.com/68321900/119004300-b9e1a700-b98e-11eb-8836-687f70fe762b.png)  
Later wordt motor uitgebreidt:  
![image](https://user-images.githubusercontent.com/68321900/119004361-c6fe9600-b98e-11eb-8ded-fa193b11e429.png)  
![image](https://user-images.githubusercontent.com/68321900/119004397-d1209480-b98e-11eb-9839-d9287f0218f5.png)  
Let op hoe we nu de motor doorgeven bij aanmaken object:  
![image](https://user-images.githubusercontent.com/68321900/119004471-e5fd2800-b98e-11eb-8426-53b4972b4e15.png)  

**Interfaces**
= referentietype, klasse, maar kan enkel het volgende bevatten:
- constanten
- abstracte methodes (zonder private,default, static, ...)  
![image](https://user-images.githubusercontent.com/68321900/119005419-ba2e7200-b98f-11eb-8aca-7c22e7647ebd.png)  
- default methodes met implementatie
- static methodes met implementatie

UML: ```<<Interface>>```

Implementatie gebeurt in subklasse, je belooft dit: ```implemets```  
![image](https://user-images.githubusercontent.com/68321900/119005834-15f8fb00-b990-11eb-87e5-4cdb8c96e7b5.png)  

VOORDEEL: een klasse kan **meerdere** interfaces implementeren maar je belooft om de abstracte methodes van die interface te implementeren

**Sorteren**
- Comparable interface: natuurlijke sorteerwijze  
  - Resultaat int < 0 --> object waar methode op aangeroepen wordt is KLEINER dan vergeleken
  - Resultaat int = 0 --> object waar methode op aangeroepen wordt is GELIJK aan vergeleken
  - Resultaat int > 0 --> object waar methode op aangeroepen wordt is GROTER dan vergeleken
```
public interface Comparable<T> {
  public int compareTo(T o);
}
//in klasse & als methode
public class X implements Comparable<X> {
  public int compareTo(X o) {
    int getal = this.attribute.compareTo(o.getAttribute()); //we onthouden de waarde van EERSTE sortering
    return getal == 0 ? this.otherAttribute.compareTo(o.getOtherAttribute()) : getal; //we sorteren verder indien eerste gelijk is
  }
}

//use the method
Collections.sort(list of objects);
```
- Comparator interface: zelf gekozen sorteerwijze 
```
public interface Comparator<T> {
  int compare(T o1, T o2);
}

//vb:
public class FirstNameComparator implements Comparator<Name> {
  public int compare(Name o1, Name o2) {
    int firstCmp = o1.getFirstName().compareTo(o2.getFirstName());
    return (firstCmp != 0 ? firstCmp : o1.getLastName().compareTo(o2.getLastName()));
  }
}

//use the method
Collections.sort(list of objects, new FirstNameComparator());
```

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
