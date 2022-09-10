### Status nicht direkt ändern

Durch das direkte ändern wird die Komponente nicht erneut gerendert.  
Stattdessen soll immer die Funktion _setState()_ verwendet werden.

```typescript jsx
    this.state.comment = "Hallo";         // Falsch, so nicht machen!
```
```typescript jsx
    this.setState({comment: "Hallo"});    // So wird ein Wert richtig gesetzt
```

Ausnahme ist das erstmalige Zuweisen im Constructor

============================================================================================

### State Updates können asynchron sein

React kann mehrere Aufrufe in einem einzigen Update zusammenfassen.  
Da "probs" und "state" asynchron aktualisiert werden können,  
sollte man sich bei der Berechnung des nächsten Zustands nicht auf ihre Werte verlassen.

```typescript jsx
    this.setState({
      counter: this.state.counter + this.props.increment, // Das ist nicht zuverlässig
    });
```

Dafür gibt es eine weitere Variante von _setState()_ die als Parameter eine Funktion hat.  
Diese Funktion erhält den vorherigen "state" als erstes Argument und als zweites Argument die "probs"

```typescript jsx
    this.setState((state, probs) => ({
      counter: this.state.counter + this.props.increment, // So wird es sicher funktionieren
    }));
```

============================================================================================

### State Updates werden zusammengefügt

Mit Aufruf von _setState()_ wird der Wert von "state" nicht überschrieben, sondern zusammengefügt.  
Hat ein "state" mehrere Variablen, können diese unabhängig voneinander verändert oder hinzugefügt werden.

```typescript jsx
constructor(props) {
  super(props);
  this.state = {
    first: "",
    second: ""
  };  
}
```
```typescript jsx
setFirst(value) {
  this.setState({first: value});
}
setSecond(value) {
  this.setState({second: value});
}
```

============================================================================================

### Daten fließen nach unten

Weder übergeordnete noch untergeordnete Komponenten können wissen,  
ob eine bestimmte Komponente zustands behaftet oder zustandslos ist,  
und es sollte ihnen egal sein, ob sie als Funktion oder als Klasse definiert ist.

Aber eine Komponente kann ihren Status als "probs" an die untergeordneten Komponenten weitergeben.

```typescript jsx
  <FormattedDate date={this.state.date} />
```

Jeder Status gehört immer einer bestimmten Komponente, und alle Daten oder Benutzeroberflächen,  
die von diesem Status abgeleitet werden, können sich nur auf Komponenten „unterhalb“ in der Struktur auswirken.