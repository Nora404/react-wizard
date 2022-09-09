### Funktions und Klassenkomponenten

Mit Komponenten kan die Benutzeroberfläche in unabhängige, wiederverwendbare Teile aufteilen werden.  
Der einfachste Weg, eine Komponente zu definieren, besteht darin, eine JavaScript-Funktion zu schreiben:

```typescript jsx
    function Welcome(props) {
        return <h1>Hello, {props.name}</h1>;
    }
```
Diese Funktion ist eine gültige React-Komponente
* Sie hat ein einzelnes "Probs"-Argument was für die Eigenschaft der Komponente steht
* Sie gibt ein React-Element zurück

```typescript jsx
    class Welcome extends React.Component {
        render() {
            return <h1>Hello, {this.props.name}</h1>;
        }
    }
```
Die meisten Komponenten sind wie diese, Klassenkomponenten
* Sie erben immer von React.Component
* Sie __müssen__ eine _render()_ Funktion haben
