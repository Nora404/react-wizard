### Bespiel an einer Uhr

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

Hier wird jede Sekunde _root.render(element)_ aufgerufen.  
Nun soll daraus eine Uhr-Komponente extrahiert werden. Diese sähe dann so aus:

```typescript jsx
    function Clock(props) {
        return (
            <div><h1>Hello, world!</h1>
                <h2>It is {props.date.toLocaleTimeString()}.</h2>    
            </div>  
        );
    }
```
Die tick-Funktion ist wesentlich schmaler geworden, wird aber noch immer jede Sekunde aufgerufen.
```typescript jsx
    function tick() {
        root.render(<Clock date={new Date()} />);
    }
```
Ziel ist es das Aktualisieren in die Clock Komponente zu bringen,  
dafür wird eine weitere Eigenschaft von Komponenten benötigt: "state"  
"state" ähnelt dem "probs" ist aber privat und wird vollständig von der Komponente kontrolliert.

============================================================================================

### Konvertieren einer Funktion in eine Klasse
* Eine ES6-Klasse erstellen, die denselben Namen hat.
* Die Klasse erbt von React.Component
* Die Methode _render()_ muss hinzugefügt werden
* Den Körper der Funktion in die Methode _render()_ einfügen
* Die Eigenschaft "probs" ersetzten durch "this.probs"
* Die Funktion löschen, sie wird nicht mehr gebraucht

```typescript jsx
class Clock extends React.Component {
    render() {
        return (
            <div>
                <h1>Hello, world!</h1>
                <h2>It is {this.props.date.toLocaleTimeString()}.</h2>
            </div>
        );
    }
}
```

Da sich _.date_ verändern soll, muss es ein Wert von "state" werden.  
Der Klasse wird dafür ein Constructor hinzugefügt.

```typescript jsx
constructor(props) {
  super(props);
  this.state = {date: new Date()};  
}
```
Der Constructor braucht den Parameter "probs" welcher mit _super(probs)_ weiter gereicht wird.  
Und es wird die Eigenschaft "state" initialisiert, welche immer ein Objekt hält.  
Auch wenn _root.render()_ die Clock-Komponente nun laden kann, wird sie sich noch nicht aktualisieren.  

```typescript jsx
class Clock extends React.Component {
  constructor(props) {    
    super(props);    
    this.state = {date: new Date()};  
  }
  
  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>      
      </div>
    );
  }
}

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<Clock />);
```
============================================================================================

### Lebenszyklus Methoden

Eine Komponente wird geladen, sie lebt, und wird wieder gelöscht. Dabei muss aufgeräumt werden.  
Der Timer soll eingerichtet werden, wenn die Komponente geladen wird.  
Wenn die Komponente gelöscht wird, soll auch der Timer gelöscht werden. Dafür gibt es Methoden.

```typescript jsx
  componentDidMount()     // Wird einmalig beim ersten Rendern ausgeführt
 
  componentDidUpdate()    // Wird ausgeführt wenn sich die Komponente verändert

  componentWillUnmount()  // Wird aufgerufen wenn die Komponente aus dem DOM entfernt wird

  componentDidCatch()     // Wird aufgerufen wenn irgendwo ein Fehler geworfen wird
```
Der Timer macht sich gut in der _componentDidMount()_ Funktion.  
Der Klasse kann manuell weitere Eigenschaften hinzugefügt werden, solange es nicht am Datenfluss teilnimmt.  
In der Funktion _componentWillUnmount()_ wird das Intervall beendet.  
Das alleinige Schließen der Komponente würde das Intervall nicht stoppen. 

```typescript jsx
componentDidMount() {
  this.timerID = setInterval(      
    () => this.tick(),      
    1000    
  );  
}
```
```typescript jsx
componentWillUnmount() {
  clearInterval(this.timerID);  
}
```

============================================================================================

### this.setState()

Mit der vom React mitgebrachten Funktion _this.setState()_ wird die Eigenschaft "state" verändert.  
Diese Eigenschaft soll nicht direkt verändert werden, nur über diese Funktion.  
Das Intervall ruft jede Sekunde den Callback _this.tick()_ auf. Sie soll den "state" aktualisieren.

```typescript jsx
  tick() {    
    this.setState({ 
      date: new Date()    
    });  
  }
```
Jetzt tickt die Uhr jede Sekunde!