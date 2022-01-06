# HTML basis deel 1 - CSS intro
Start website: ! + tab
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    
</body>
</html>
```
Bij een image:
- alt-attribuut (**verplicht**): korte beschrijving image (slechtzienden)
- title-attribuut: uitgebreide beschrijving en zorgt voor tooltip

Code formatteren:
- shift + alt + f

Shortcuts:
- h1 + tab = ```<h1></h1>```
- i + tab = ```<i></i>```
- img + tab = ```<img src alt="">```

CSS selectors:
- type = ```div { ... }```
- class = ```.class { ... }```
- id = ```#id { ... }```
- group = ```h1, .class, a { ... }```

# HTML basis deel 2
Websites:
- MDN references: https://developer.mozilla.org/en-US/docs/Web/HTML
- Validator: https://validator.w3.org/

Lijsten:
- Ordered: ```<ol>```
  - item: ```<li>```
- Unordered: ```<ul>```
  - item: ```<li>```
- Definitie lijst: ```<dl>```
  - term: ```<dt>```
  - beschrijving: ```<dd>```

```<div>```: block element, algemene container, elementen groeperen
```<span>```: inline element, algemene container

## Text block-level elements
```<blockquote>``` = lange citaten  
```<figure>``` = groepeert illustratie met bijschrift ```<figcaption>```  
```<address>``` = adres contact informatie  
```<pre>``` = behouden tabs, witruimte in code  
```<hr>``` = thematische scheiding tussen paragrafen  

## Text inline elements
```<strong>``` = vet  
```<em>``` = cursief  
```<b>``` = aandacht lezer op tekst bestigen (soort vet maar minder belangrijk dan strong)  
```<i>``` = soort cursief maar minder belangrijk  
```<small>``` = aanvullende informatie  
```<cite>``` = markeren van de naam auteur of creatief werk  
```<q>``` = korte citaten in lopende zin (quote) -> gebruik cite om bron te vermelden  
```<abbr>``` = afkorting  
```<dfn>``` = markeert de eerste keer dat een definitie voorkomt  
```<code>``` = markeren van programma code  
```<time>``` = tijdstip/datum aanduiden  
```<samp>``` = computer uitvoer  
```<kbd>``` = gebruikersinvoer  
```<s>``` = informatie die niet meer klopt (suppress)  
```<sub>``` = subscript  
```<sup>``` = superscript  
```<mark>``` = markeer tekst  
```<ins>``` = geeft aan dat inhoud is toegevoegd  
```<del>``` = geeft aan dat inhoud is verwijderd  

## Hyperlinks
```target="_blank"``` = opent link in nieuw tabblad  
```href="mailto:verplanckerobin@gmail.com"``` = link naar mail adres  
```href="tel:+157280394"``` = link naar telefoonnr  
```href="./pdf/h05.pdf"``` = pdf weergeven in browser  
```href="./pdf/h05.pdf" download="h5"``` = downloaden van pdf  

## Paginastructuur
- sectioning content:
  - ```<article>``` = zelfstandig stuk inhoud, onafhankelijk te hergebruiken
  - ```<aside>``` = zijdelingse informatie
  - ```<nav>``` = hoofdnavigatie
  - ```<section>``` = onderdeel van een pagina waarvoor geen specifiek element is
  - ```<header>``` = kopgedeelte
  - ```<footer>``` = voetgedeelte  

![image](https://user-images.githubusercontent.com/68321900/148380138-0c69978d-175b-49d5-94b9-ec20b8933257.png)

## Speciale karakters  
![image](https://user-images.githubusercontent.com/68321900/148380668-dd924fb0-ccdd-4df0-95d4-6886739922a8.png)

Pictogrammen tabblad (favicon): ![image](https://user-images.githubusercontent.com/68321900/148380814-85b9556d-5886-4e22-a0ef-f641879dec58.png)

# Tabellen en formulieren
## Tabellen
```<table>```
- ```<tr>``` = table row
  - ```<th>``` = cel voor hoofding 
  - ```<td>``` = cel met data

Rand rond tabel en cellen:
```
table, th, td {
  border: 1px solid black;
}

//Verwijder dubbele rand
table {
  border-collapse: collapse;
}

```
- Voor witruimte gebruik je padding
- ```<td colspan="x">``` = cellen spreiden over kolommen
- ```<td rowspan="x">``` = cellen spreiden over rijen

Logische indeling voor een tabel:
- ```<thead>```
- ```<tbody>```
- ```<tfoot>```

Titel voor tabel (bijschrift): ```<caption>```
- Plaats wijzigen met CSS ```caption-side: location;```

```<colgroup>``` = 1 of meerdere kolommen uit de tabel groeperen voor opmaak

## Formulieren
```<form action="..." method="...">```  
- **action**: geeft aan naar waar de data gestuurd wordt na het klikken op de verzendknop
  - Kan ook een mailadres zijn: action = "mailto:...?subject=..." enctype="text/plain"
- **method**: bepaalt de HTTP methode die gebruikt wordt bij het verzenden van de formulier-data
  - get: 
  - post: gebruik dit
- **id of name**: voor CSS opmaak
- **autocomplete**: voor de velden in het formulier
- **novalidate**: de data moet niet gevalideerd worden voor het formulier gesubmit wordt
 
```<input>``` = form control tag
- attribuut **type** bepaalt het type form control
- name: belangrijk! Deze naam wordt met de waarde doorgestuurd
- id: voor opmaak en labels
- value: belangrijk voor form controls waarin de gebruiker zelf niet typt

Bij radio button of checkbox is er het attribuut **checked**

Keuzelijst:  
![image](https://user-images.githubusercontent.com/68321900/148395227-c1a0d7c9-c3f0-4ca8-bb71-30adca9719d1.png)  
- multiple om meerdere keuzes toe te laten
- size om meerdere opties te tonen

Datalijst:  
![image](https://user-images.githubusercontent.com/68321900/148395402-f6a3cda7-974c-4d42-a987-626c55d0f8c1.png)  

Attributen:
- placeholder: hint geven
- ```<label>``` = tekst die bij een form control hoort linken:  
  ```
  <label>
    Tekst blabla
    <input .../>
  </label>
  ```
- required: veld is verplicht
- bij **type number** kan een min/max waarde meegegeven worden

Form controls groeperen: ```<fieldset>``` en ```<legend>```

# CSS basis deel 1
CSS toevoegen aan HTML:
- external: via link
- internal: binnen <style> tags
- inline: met een style attribuut
  
Background:
- -image
- -repeat: herhalen afbeelding tot alle ruimte gevuld is
  - repeat-x
  - repeat-y
  - no-repeat
  - space
  - round
- -attachment
  - fixed
  - scroll
  - local
- -position
- -clip
- -origin
- -size
- linear-gradient
- radial-gradient
  
Lijsten:
 

  

































