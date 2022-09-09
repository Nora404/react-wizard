
    const element = <h1>Hallo Welt</h1>

Diese Syntax ist weder ein String noch HTML, es nennt sich jsx.
Es ist eine Erweiterung von JavaScript, die in React für die UI benutzt wird.
Es ist kein Muss für React, aber sehr verbreitet und hilfreich.

////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

### Ausdrücke in JSX einbetten:

    > const name = 'Foo Bar';
    > const element = <h1>Hallo, {name}</h1>

In den geschweiften Klammern {} steht ein JS Ausdruck.
Das kann auch {2+2} sein, oder {getUser(name)}

////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

### JSX ist auch ein Ausdruck:

    > getGreeting(name){
    >     if(user){
    >         return <h1>Hallo, {getUser(name)}</h1>;
    >     } else {
    >         return <h1>Hallo, Fremder</h1>;
    >     }
    > }

JSX kann verwendet werden innerhalb von Schleifen, Bedingungen, Variablen oder Argumenten.
Sie können als Ergebnis einer Funktion zurückgegeben werden.

////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

### Angabe von Attributen mit JSX

    > const element = <a href="https://www.reactjs.org"> link </a>;

Eine Variante sind Anführungszeichen um Strings als Attribute anzugeben.
Eine andere Variante sind die geschweiften Klammern.

    > const element = <img src={user.avatarUrl}></img>;

In einem Attribut sollten nicht beide Varianten gemischt verwendet werden.
React benutzt die camelCase Schreibweise für Eigenschaften, anstelle von HTML Attributnamen.
Zum Beispiel aus "class" wird "className" oder aus "tabindex" wird "tabIndex"

////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

### Tags schließen

    > const element = <img src={user.avatarUrl} />;

Ist zwischen dem Tag nichts, kann es sofort mit /> geschlossen werden.
Es ist auch möglich Tags zu verschachteln, also das die Kinderknoten haben.

////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

### JSX sind Objekte

Bis auf React.createElement() werden alle JSX in Objekten kompiliert.
Die folgenden Beispiele sind identisch:

    > const element = (                     const element = React.createElement(
    >   <h1 className="greeting">               'h1',
    >    Hello, world!                          {className: 'greeting'},
    >  </h1>                                    'Hello, world!'
    > );                                    );

Daraus wird dieses "React-Element" erstellt:

    > const element = {
    >   type: 'h1',
    >   props: {
    >     className: 'greeting',
    >     children: 'Hello, world!'
    >   }
    > };






