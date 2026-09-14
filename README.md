# ⚛️ React Playground

Este repositório foi criado como parte de um **Projeto Integrado**, com o objetivo de apresentar e explorar os principais conceitos do **React** e seu ecossistema.

A proposta não é construir uma aplicação complexa, mas utilizar pequenos exemplos práticos para entender:

* O que é React;
* Por que ele é utilizado;
* Como uma aplicação React é estruturada;
* Componentes;
* JSX;
* Props;
* Estado;
* Eventos;
* Renderização condicional;
* Renderização de listas;
* Hooks básicos;
* Comunicação entre componentes;
* Consumo de APIs;
* Principais vantagens e desvantagens.

---

# 📚 O que é React?

React é uma **biblioteca JavaScript para construção de interfaces de usuário**.

Ele foi criado pelo Facebook, atualmente Meta, e é utilizado principalmente para construir aplicações web baseadas em **componentes reutilizáveis**.

Em vez de construir uma página inteira como um único bloco, React incentiva dividir a interface em pequenas partes independentes.

Por exemplo:

```text
Aplicação
│
├── Header
│
├── Sidebar
│
└── ProductList
    │
    ├── ProductCard
    ├── ProductCard
    └── ProductCard
```

Cada uma dessas partes pode ser um componente React.

---

# 🧩 Componentes

Componentes são uma das ideias centrais do React.

Um componente é uma parte reutilizável da interface.

```jsx
function Button() {
  return <button>Clique aqui</button>;
}
```

Depois podemos utilizar esse componente:

```jsx
function App() {
  return (
    <div>
      <Button />
      <Button />
    </div>
  );
}
```

Isso permite dividir interfaces grandes em pequenas partes mais fáceis de entender e manter.

---

# 📝 JSX

React utiliza uma sintaxe chamada **JSX**.

Ela permite escrever uma estrutura semelhante a HTML dentro do JavaScript.

```jsx
function Welcome() {
  const name = "Gustavo";

  return <h1>Olá, {name}!</h1>;
}
```

As chaves `{}` permitem utilizar expressões JavaScript dentro do JSX.

```jsx
const age = 20;

return <p>Idade: {age}</p>;
```

Apesar da aparência, JSX **não é HTML**. Ele é transformado em JavaScript durante o processo de build da aplicação.

---

# 📦 Props

**Props** são utilizadas para enviar informações de um componente para outro.

Podemos pensar nelas como os parâmetros de uma função.

```jsx
function User({ name }) {
  return <p>Usuário: {name}</p>;
}
```

Utilizando o componente:

```jsx
<User name="Maria" />
<User name="João" />
<User name="Carlos" />
```

O mesmo componente pode apresentar informações diferentes dependendo das propriedades recebidas.

---

# 🔄 Estado

Nem toda informação de uma interface permanece igual.

Imagine um contador:

```text
Contador: 0
```

Depois de clicar:

```text
Contador: 1
```

Para armazenar informações que podem mudar durante a utilização do componente, React possui o conceito de **estado**.

Um dos hooks mais utilizados para isso é o `useState`.

```jsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Contador: {count}</p>

      <button onClick={() => setCount(count + 1)}>
        Incrementar
      </button>
    </div>
  );
}
```

Quando o estado é alterado, React atualiza a interface para representar o novo valor.

---

# 🖱️ Eventos

React permite responder às interações realizadas pelo usuário.

Alguns exemplos:

```text
onClick
onChange
onSubmit
onFocus
onBlur
```

Exemplo:

```jsx
function Button() {
  function handleClick() {
    alert("Botão clicado!");
  }

  return (
    <button onClick={handleClick}>
      Clique aqui
    </button>
  );
}
```

---

# 👁️ Renderização condicional

É comum precisar mostrar ou esconder elementos dependendo de alguma condição.

```jsx
function UserStatus({ logged }) {
  return (
    <div>
      {logged ? (
        <p>Usuário autenticado</p>
      ) : (
        <p>Faça login</p>
      )}
    </div>
  );
}
```

Também podemos utilizar operadores como `&&`.

```jsx
{isAdmin && <button>Excluir usuário</button>}
```

---

# 📋 Renderização de listas

Interfaces frequentemente precisam representar coleções de dados.

Por exemplo:

```jsx
const users = [
  { id: 1, name: "Ana" },
  { id: 2, name: "Carlos" },
  { id: 3, name: "Maria" },
];
```

Podemos utilizar `map` para transformar esses dados em elementos:

```jsx
function UserList() {
  return (
    <ul>
      {users.map((user) => (
        <li key={user.id}>
          {user.name}
        </li>
      ))}
    </ul>
  );
}
```

A propriedade `key` ajuda o React a identificar cada elemento da lista durante as atualizações da interface.

---

# 🪝 Hooks

Hooks são funções disponibilizadas pelo React para utilizar determinados recursos dentro de componentes.

Para uma introdução ao React, dois hooks são especialmente importantes.

## useState

Utilizado para armazenar estado.

```jsx
const [name, setName] = useState("");
```

## useEffect

Permite executar determinados efeitos relacionados ao ciclo de vida do componente ou à alteração de dependências.

Exemplo simples:

```jsx
import { useEffect } from "react";

function App() {
  useEffect(() => {
    console.log("Componente carregado");
  }, []);

  return <h1>Hello React</h1>;
}
```

Existem diversos outros hooks no ecossistema React, mas `useState` e `useEffect` já permitem compreender boa parte dos exemplos básicos.

---

# 🔗 Comunicação entre componentes

Uma aplicação React normalmente possui vários componentes trabalhando juntos.

Uma abordagem muito comum é:

```text
Parent
  │
  │ props
  ▼
Child
```

O componente pai pode enviar informações para o filho através de props.

```jsx
function App() {
  const username = "Gustavo";

  return <Profile name={username} />;
}

function Profile({ name }) {
  return <h2>{name}</h2>;
}
```

O pai também pode enviar funções:

```jsx
function App() {
  function handleSave() {
    console.log("Salvando...");
  }

  return <Button onSave={handleSave} />;
}

function Button({ onSave }) {
  return (
    <button onClick={onSave}>
      Salvar
    </button>
  );
}
```

Esse fluxo ajuda a manter previsível a comunicação entre os componentes.

---

# 🌐 Consumindo uma API

Aplicações frontend normalmente precisam buscar informações de um backend.

Isso pode ser feito utilizando a API `fetch` do navegador.

```jsx
import { useEffect, useState } from "react";

function Users() {
  const [users, setUsers] = useState([]);

  useEffect(() => {
    async function loadUsers() {
      const response = await fetch(
        "https://jsonplaceholder.typicode.com/users"
      );

      const data = await response.json();

      setUsers(data);
    }

    loadUsers();
  }, []);

  return (
    <ul>
      {users.map((user) => (
        <li key={user.id}>
          {user.name}
        </li>
      ))}
    </ul>
  );
}
```

O fluxo simplificado é:

```text
React
  │
  │ HTTP Request
  ▼
API
  │
  │ JSON
  ▼
React
  │
  ▼
Atualiza estado
  │
  ▼
Renderiza interface
```

---

# 🏗️ Estrutura básica de um projeto

Uma aplicação pequena poderia possuir a seguinte organização:

```text
src/
│
├── components/
│   ├── Button/
│   ├── Header/
│   └── UserCard/
│
├── pages/
│   ├── Home/
│   └── Users/
│
├── services/
│   └── api.js
│
├── App.jsx
└── main.jsx
```

Não existe uma única estrutura obrigatória para projetos React.

Conforme uma aplicação cresce, sua organização também pode evoluir.

---

# 🌎 O ecossistema React

React é responsável principalmente pela construção da **interface**.

Em aplicações reais, normalmente outras bibliotecas e ferramentas são adicionadas conforme as necessidades do projeto.

```text
                    React
                      │
        ┌─────────────┼─────────────┐
        │             │             │
      Build        Routing        Estado
        │             │             │
      Vite       React Router    Zustand
                                    │
                              TanStack Query
```

Algumas ferramentas comuns são:

| Ferramenta     | Objetivo                              |
| -------------- | ------------------------------------- |
| React          | Construção da interface               |
| Vite           | Desenvolvimento e build               |
| React Router   | Navegação entre páginas               |
| TypeScript     | Tipagem estática                      |
| TanStack Query | Gerenciamento de dados vindos de APIs |
| Zustand        | Gerenciamento de estado               |
| Tailwind CSS   | Estilização                           |
| Vitest         | Testes                                |
| Next.js        | Framework baseado em React            |

Essas ferramentas **não são obrigatórias para utilizar React**.

Uma das características do ecossistema é justamente permitir que cada projeto escolha as ferramentas adequadas para suas necessidades.

---

# ⚛️ React não é um framework completo

É importante diferenciar React de frameworks como **Next.js**.

React fornece principalmente ferramentas para criação e atualização da interface.

Recursos como:

* roteamento;
* estrutura de aplicação;
* renderização no servidor;
* otimização de imagens;
* estratégias de cache;
* endpoints de backend;

podem depender de outras ferramentas.

Frameworks como Next.js utilizam React como base e adicionam várias dessas funcionalidades.

```text
Next.js
┌─────────────────────────┐
│                         │
│          React          │
│                         │
│ + Routing               │
│ + Server Rendering      │
│ + Backend               │
│ + Otimizações           │
│ + Estrutura             │
│                         │
└─────────────────────────┘
```

---

# 🧠 Virtual DOM

Uma expressão bastante associada ao React é **Virtual DOM**.

De forma simplificada, React mantém uma representação da interface e, quando algum estado muda, determina quais partes precisam ser atualizadas.

Por exemplo:

```text
Antes

Contador: 0
```

Depois:

```text
Contador: 1
```

React não precisa recriar manualmente toda a página para representar essa mudança.

O desenvolvedor declara **como a interface deve ficar para determinado estado**, e React cuida do processo de atualização.

Essa característica está relacionada ao modelo **declarativo** do React.

---

# 📢 Programação declarativa

Em JavaScript tradicional, poderíamos escrever:

```javascript
const button = document.querySelector("#button");
const counter = document.querySelector("#counter");

let value = 0;

button.addEventListener("click", () => {
  value++;
  counter.innerText = value;
});
```

Estamos dizendo diretamente ao navegador quais elementos devem ser modificados.

Com React:

```jsx
function Counter() {
  const [count, setCount] = useState(0);

  return (
    <>
      <p>{count}</p>

      <button onClick={() => setCount(count + 1)}>
        Incrementar
      </button>
    </>
  );
}
```

Nós descrevemos:

> Para este estado, a interface deve ser assim.

Quando o estado muda, React atualiza a interface.

---

# ✅ Vantagens

### 🧩 Componentização

Aplicações podem ser divididas em componentes menores e reutilizáveis.

Isso facilita organização, manutenção e reaproveitamento de código.

### ♻️ Reutilização

Um mesmo componente pode ser utilizado em diferentes lugares.

```jsx
<Button>Salvar</Button>
<Button>Editar</Button>
<Button>Excluir</Button>
```

### 🌎 Ecossistema

React possui um ecossistema muito grande de bibliotecas, ferramentas, documentação e conteúdo educacional.

### 👥 Comunidade

Por ser amplamente utilizado, existe uma grande comunidade e muitos materiais disponíveis.

### 📦 Flexibilidade

React não força uma arquitetura única.

O projeto pode escolher suas próprias ferramentas para:

* estado;
* estilização;
* formulários;
* requisições;
* testes;
* roteamento.

### 💼 Mercado

React é amplamente utilizado no desenvolvimento frontend profissional, tornando seu conhecimento relevante para quem deseja trabalhar com aplicações web.

### 📱 React Native

Conhecimentos adquiridos com React também facilitam o aprendizado de React Native para desenvolvimento de aplicações mobile.

---

# ❌ Desvantagens

### 🧩 React resolve apenas parte do problema

React é focado principalmente na interface.

Projetos normalmente precisam adicionar outras bibliotecas para resolver necessidades como roteamento, formulários, gerenciamento de estado e comunicação com APIs.

---

### 🌎 Ecossistema muito grande

A flexibilidade também pode gerar dúvidas.

Por exemplo, diferentes projetos podem utilizar:

```text
Redux
Zustand
Context API
MobX
```

para resolver problemas semelhantes.

Para iniciantes, tantas opções podem dificultar a escolha.

---

### 📚 Curva de aprendizado

Aprender JSX e componentes costuma ser relativamente simples.

Porém, aplicações maiores exigem conhecimento de outros conceitos:

```text
JavaScript
TypeScript
HTTP
APIs
Estado
Roteamento
Build
Testes
Arquitetura
```

Portanto, aprender React não significa aprender apenas uma biblioteca.

---

### 🔄 Atualizações do ecossistema

React e suas ferramentas evoluem constantemente.

Bibliotecas populares, padrões e recomendações podem mudar com o tempo, exigindo atualização frequente dos desenvolvedores.

---

### 🏗️ Liberdade arquitetural

A ausência de uma estrutura obrigatória pode ser positiva em projetos experientes, mas também pode resultar em aplicações desorganizadas quando não existem padrões definidos pela equipe.

---

# ⚖️ Quando React faz sentido?

React pode ser uma boa escolha para:

* aplicações web interativas;
* dashboards;
* sistemas administrativos;
* plataformas SaaS;
* e-commerce;
* aplicações com interfaces complexas;
* aplicações que possuem muitos componentes reutilizáveis.

Para páginas extremamente simples e praticamente estáticas, utilizar React pode adicionar uma complexidade desnecessária.

---

# 🧪 Objetivo deste Playground

Este projeto contém pequenos exemplos independentes para demonstrar os conceitos apresentados.

Uma possível organização é:

```text
src/
│
├── examples/
│   │
│   ├── 01-component/
│   ├── 02-props/
│   ├── 03-state/
│   ├── 04-events/
│   ├── 05-conditional-rendering/
│   ├── 06-lists/
│   ├── 07-use-effect/
│   ├── 08-form/
│   └── 09-api/
│
└── App.jsx
```

A ideia é permitir que cada conceito seja executado e modificado durante a apresentação.

---

# 🚀 Executando o projeto

Clone o repositório:

```bash
git clone <URL_DO_REPOSITORIO>
```

Entre na pasta:

```bash
cd react-playground
```

Instale as dependências:

```bash
npm install
```

Execute o projeto:

```bash
npm run dev
```

Abra o endereço informado pelo terminal no navegador.

---

# 🎯 Conceitos apresentados

Ao final deste playground, esperamos compreender:

* O que é React;
* O que é um componente;
* Como JSX funciona;
* Como utilizar props;
* Como utilizar estado;
* Como responder a eventos;
* Como renderizar conteúdo condicionalmente;
* Como renderizar listas;
* O funcionamento básico de hooks;
* Como componentes se comunicam;
* Como consumir uma API;
* Como React se encaixa em seu ecossistema;
* Quando React pode ou não ser uma boa escolha.

---

# 📖 Conclusão

React oferece uma abordagem baseada em **componentes, estado e interfaces declarativas** para desenvolvimento frontend.

Sua principal força não está apenas na biblioteca, mas também no grande ecossistema existente ao seu redor.

Ao mesmo tempo, essa flexibilidade exige decisões sobre arquitetura e ferramentas adicionais, principalmente conforme a aplicação cresce.

Por isso, entender React não significa apenas decorar sua API, mas compreender conceitos fundamentais como:

```text
Componentes
     +
   Props
     +
   Estado
     +
  Eventos
     +
Renderização
     =
Interface React
```

Este playground foi criado justamente para experimentar esses conceitos de forma simples e prática.
