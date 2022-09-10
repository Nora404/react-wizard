### Funktions und Klassenkomponenten

Mit Komponenten kan die Benutzeroberfläche in unabhängige, wiederverwendbare Teile aufteilen werden.  
Der einfachste Weg, eine Komponente zu definieren, besteht darin, eine JavaScript-Funktion zu schreiben.  
_Komponenten-Namen beginnen immer mit einem Großbuchstaben_

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

============================================================================================

### Rendern einer Komponente

```typescript jsx
    const element = <Welcome name="Sara" />;
```
Der Name einer Komponente wird in Tags geschrieben, seine Argumente sehen aus wie HTML-Attribute.  
JSX-Attribute und untergeordnete Elemente werden als einzelnes Objekt übergeben ("probs").

```typescript jsx
    function Welcome(props) {  
        return <h1>Hello, {props.name}</h1>;
    }
    
    const root = ReactDOM.createRoot(document.getElementById('root'));
    const element = <Welcome name="Sara" />;
    root.render(element);
```
============================================================================================

### Komponenten zusammenstellen

Eine Schaltfläche, ein Formular, ein Dialog, ein Bildschirm:  
In React-Apps werden all dies üblicherweise als Komponenten ausgedrückt.  
Komponenten können auf andere Komponenten verweisen.  

```typescript jsx
    function Welcome(props) {
        return <h1>Hello, {props.name}</h1>;
    }
    
    function App() {
        return (
        <div>
            <Welcome name="Sara" />      
            <Welcome name="Cahal" />      
            <Welcome name="Edite" />    
        </div>
        );
    }
```

============================================================================================

### Komponenten extrahieren

Wenn ein Teil der Benutzeroberfläche mehrmals verwendet wird ( Button, Panel, Avatar)  
oder allein komplex genug ist (App, FeedStory, Comment), ist er ein guter Kandidat,  
um in eine separate Komponente extrahiert zu werden.

```typescript jsx
    function Comment(props) {
        return (
            <div id="comment">
                <img id="Avatar"
                     src={probs.author.avatarUrl}
                     alt={probs.author.avatar}/>
            </div>
            <div id="name"> {probs.author.name} </div>
            <div id="date"> {probs.date} </div>
            <div id="text"> {probs.text} </div>
        );
    }
```
In diesem Beispiel kann eine Avatar-Komponente extrahiert werden.

```typescript jsx
    function Avatar(props) {
        return (
            <img id="Avatar"
                 src={probs.user.avatarUrl}
                 alt={probs.user.avatar}/>
        );
    }
```
Der neue Code sieht dann so aus:

```typescript jsx
    function Comment(props) {
        return (
            <div id="comment"> <Avatar user={probs.author} /> </div>
            <div id="name"> {probs.author.name} </div>
            <div id="date"> {probs.date} </div>
            <div id="text"> {probs.text} </div>
        );
    }
```