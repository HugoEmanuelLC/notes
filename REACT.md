# Aide-mémoire pour apprendre React JS

[www.reactjs.wiki]

## Installation

* npx create-react-app .
* npx create-react-app name-app

* npm run build
* npm start
* http://localhost:3000/

### JSX

Comprendre la syntaxe jsx,
c'est du js classic où on peut rajouter la structure html qui sera convertit par le blander (vite)

- vite 
    * npm create vite@latest ./
    * npm create vite@latest ./ --template blank 
    * npm i
    * npm run dev

***extention chrome -> react dev tools***

## Composants

### Création d'un composant

Exemples:

le style tjrs dans un objet
les atributs tjrs en camelcase (pas les: aria- , ou data-)

```jsx
const varTitle = "Bonjour les gens"

function App(){
    return <>
        <h1 id="title" className="title" style={{color: 'red', backgroundColor: 'blue'}}>
            {varTitle}
        </h1>
        <p>
            text
        </p>
    </>
}

export default App
```

Exemples:

tjrs avoir des balises fermente
(<input />) ou (<input> <input/>)

```jsx
const varTitle = "Bonjour les gens"
const style = {color: 'red', backgroundColor: 'blue'}

function App(){
    return <>
        <h1 id="title" className="title" style={style}>
            {varTitle}
        </h1>
        <input type="text" />
        <p>
            text
        </p>
    </>
}

export default App
```

### Evenements d'un composant

Exemples:

atributs relie aux evenements
onNameEvent (onClick ...)

```jsx
const varTitle = "Bonjour les gens"
const style = {color: 'red', backgroundColor: 'blue'}

function App(){

    const handleClick = (e)=>{
        console.log(e)
        alert("j'ai cliqué sur le titre !")
    }

    return <>
        <h1 onClick={handleClick} id="title" className="title" style={style}>
            {varTitle}
        </h1>
        <p>
            text
        </p>
    </>
}

export default App
```

Exemples:

logique conditionnel

```jsx
const varTitle = "Bonjour les gens"
const style = {color: 'red', backgroundColor: 'blue'}
const showTitle = false

function App(){

    const handleClick = (e)=>{
        console.log(e)
        alert("j'ai cliqué sur le titre !")
    }

    return <>
        {/* si showTitle = true, h1 affiché, si false h1 non affiché */}
        {showTitle && <h1 onClick={handleClick} id="title" className="title" style={style}>
            {varTitle}
        </h1>}
        <p>
            text
        </p>
    </>
}

export default App
```

Exemples:

logique conditionnel, ternaire

```jsx
const varTitle = "Bonjour les gens"
const style = {color: 'red', backgroundColor: 'blue'}
const showTitle = false

function App(){

    const handleClick = (e)=>{
        console.log(e)
        alert("j'ai cliqué sur le titre !")
    }

    return <>
        {/* si showTitle = true, h1 affiché, si false h1 non affiché */}
        {showTitle ? 
            <h1 onClick={handleClick} id="title" className="title" style={style}>
                {varTitle}
            </h1> : 
            <p>Demo</p>}
        <p>
            text
        </p>
    </>
}

export default App
```

Exemples:

list automatique

```jsx
const varTitle = "Bonjour les gens"
const style = {color: 'red', backgroundColor: 'blue'}
const showTitle = false
const todos = [
    'presenter react',
    'presenter le jsx',
    'creer des composants'
]

function App(){

    const handleClick = (e)=>{
        console.log(e)
        alert("j'ai cliqué sur le titre !")
    }

    return <>
        {/* si showTitle = true, h1 affiché, si false h1 non affiché */}
        {showTitle ? 
            <h1 onClick={handleClick} id="title" className="title" style={style}>
                {varTitle}
            </h1> : 
            <p>Demo</p>}
        <p>
            text
        </p>
        <ul>
            {/* function map:  prend un tableau en entree et pour chaque element du tableau elle va effectuer une function de transformation*/}

            {/* dans cette cituation chaque element de la liste doit avoir une "key" propre */}
            {todos.map(todo => (<li key={todo}>{todo}</li>))}
        </ul>
    </>
}

export default App
```


### Creation d'un composant

Exemples:

```jsx

function App(){
    return <>
        <Title color="red" />
        <p>
            text
        </p>
    </>
}

// objet props
// function Title (props) {
//     return <h1>Bonjour les gens</h1>
// }

function Title ({color}) {
    return <h1 style={{color: color}}>Bonjour les gens</h1>
}

export default App
```

Exemples:

```jsx

function App(){
    return <>
        <Title color="red">Mon composant</Title>
        <p>
            text
        </p>
    </>
}

function Title ({color, children}) {
    return <h1 style={{color: color}}>{children}</h1>
}

export default App
```

Exemples:

hidden

```jsx

function App(){
    return <>
        <Title color="red" hidden>Mon composant</Title>
        <p>
            text
        </p>
    </>
}

function Title ({color, children, hidden}) {
    console.log(hidden)
    // si hidden existe on affiche rien, s'il existe pas on affiche le h1
    if(hidden){
        return null
    }else{
        return <h1 style={{color: color}}>{children}</h1>
    }
    
}

export default App
```

Exemples:
spread operator

```jsx
function App(){
    return <>
        <Title color="red" hidden>Mon composant</Title>
        <p>
            text
        </p>
    </>
}

function Title ({color, children, hidden}) {
    if(hidden){
        return null
    }

    const props = {
        id: 'monid',
        className: 'maclass'
    }

    return <h1 {...props} style={{color: color}}>{children}</h1>
    
}

export default App
```


Exemples:
spread operator

```jsx
function App(){
    return <>
        <Title color="red" id="monid" className="demo">Mon composant</Title>
        <p>
            text
        </p>
    </>
}

function Title ({color, hidden, ...props}) {
    if(hidden){
        return null
    }

    console.log(props); // {id: "monid", className: "demo", children: "Mon composant"}

    return <h1 style={{color: color}} {...props} />
    
}

export default App
```