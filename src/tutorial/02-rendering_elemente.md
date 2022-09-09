
```typescript jsx
    const element = <h1>Hallo Welt</h1>;
```
    
Im Gegensatz zu Browser-DOM-Elemente sind React-Elemente einfache Objekte.  
React-DOM kümmert sich um die Aktualisierung des DOM mit React-Elementen.

__! React-Elemente sind keine Komponenten, Komponenten bestehen aus React-Elemente !__

============================================================================================

### Rendern eines Elements

```typescript jsx
    <div id="root"></div>
```

Dies steht irgendwo in der HTML-Datei, in diesem div steht alles, was vom React-DOM verwaltet wird.  
React-Anwendungen haben für gewöhnlich nur einen Root-DOM-Knoten.

Um das React-Element zu rendern wird es zuerst das DOM-Element dem _ReactDOM.createRoot()_ übergeben.  
Dann wird das React-Element an _root.render()_ übergeben.

```typescript jsx
    const root = ReactDOM.createRoot(document.getElementById('root'));
    const element = <h1>Hello, world</h1>;
    root.render(element);
```

============================================================================================

### Aktualisierung des gerenderten Elements

React-Elemente sind nicht veränderbar, sie repräsentieren einen Moment der Benutzeroberfläche.  
Eine Idee wäre dem _root.render()_ immer wieder neue Elemente zu geben,  
für gewöhnlich wird diese Funktion aber nur einmal aufgerufen.  

```typescript jsx
    const root = ReactDOM.createRoot(document.getElementById('root'));
    
    function tick() {
        const element = (
            <div>
                <h1>Hello, world!</h1>
                <h2>It is {new Date().toLocaleTimeString()}.</h2>
            </div>
        );
    root.render(element);
    }
    
    setInterval(tick, 1000);
```

Die richtige Lösung sind "Zustands behaftete Komponenten." 

