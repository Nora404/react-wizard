### Unterschiede zu HTML-Ereignissen

* React Events werden in CamelCase statt in Kleinbuchstaben geschrieben.
* Bei JSX ist der Event-Handler keine Zeichenfolge, sondern eine Funktion.

```typescript jsx
  <button onclick="nextPage()">
    HTML Event
  </button>
```
```typescript jsx
  <button onClick={nextPage}> 
    React Event
  </button>
```
In HTML ist ein _return false_ im Eventaufruf möglich, nicht aber in React.  
Um das Standardverhalten eines Events zu verhindern, muss _preventDefault_ aufgerufen werden.

```typescript jsx
  function nextPage(e) {
    e.preventDefault();    
    console.log('Auf zur nächsten Seite');
  }
```
Events brauchen in React keinen _addEventListener_, diese werden beim Rendern des Elements bereitgestellt.  
Es ist ein gängiges Muster dass, ein Event-Handler eine Methode der React-Klasse ist.

============================================================================================

### Event-Handler binden

```typescript jsx
class Toggle extends React.Component {
  constructor(props) {
    super(props);
    this.state = {isToggleOn: true};

    // Dieses Binding ist notwendig, damit 'this' im Callback funktioniert
    this.handleClick = this.handleClick.bind(this);  
  }

  handleClick() {    
    // prevState() ist fast das selbe wie setState(), der Unterschied ist 
    // dass hier der Status basierend vom vorherigen Status geändert werden soll
    this.setState(prevState => ({      
      isToggleOn: !prevState.isToggleOn    
    }));  
  }
  
    render() {
      return (
        <button onClick={this.handleClick}>        
          {this.state.isToggleOn ? 'ON' : 'OFF'}
        </button>
      );
    }
  }
```

In JavaScript sind Klassenmethoden nicht gebunden,  
wenn _this.handleClick_ ohne Bindung übergeben wird, dann hat 'this' den Wert undefined.  
Generell müssen Funktionen auf die ohne () verwiesen werden, vorher gebunden werden.

Alternative könnte auch eine Pfeilfunktion benutzt werden.

```typescript jsx
    render() {
      return (
        <button onClick={() => this.handleClick()}>    
          {this.state.isToggleOn ? 'ON' : 'OFF'}
        </button>
      );
    }
  }
```
Der Nachteil an dieser Syntax ist, bei jedem Rendern dieser Komponente wird ein anderer Callback erstellt.  
Wenn aber der Callback als "probs" an untere Komponenten weiter gegeben wird, erzeugt das wieder ein Rendern.

============================================================================================

### Übergeben von Argumenten an Event-Handler

Wenn zum Beispiel eine ID übergeben werden soll, gibt es dafür zwei Möglichkeiten.

```typescript jsx
  <button onClick={(e) => this.deleteRow(id, e)}>
    Lösche Zeile
  </button>

  <button onClick={this.deleteRow.bind(this, id)}>
    Lösche Zeile
  </button>
```

In beiden Fällen wird das "e" Argument, welches das React-Event darstellt, als zweites Argument übergeben.  
Bei der Pfeilfunktion muss das "e" explizit mit übergeben werden,  
bei _bind_ werden alle weiteren Argumente automatisch weitergeleitet. 