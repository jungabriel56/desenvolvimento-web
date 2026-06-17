## Funcionamento
- Faz uso de [[componentes]]
- Utiliza a estrutura [[SPA]] (Single Page Application)
- Conteúdo é inserido na página via JavaScript
## Hook
**Hooks** são funções introduzidas no **React 16.8** que permitem acessar recursos do framework, como **estado** e **ciclo de vida**, diretamente em **componentes funcionais**, eliminando a necessidade de escrever classes. 

Eles funcionam como "ganchos" que conectam a lógica do componente aos recursos internos do React, permitindo:

- **Gerenciamento de Estado:** Usar o `useState` para armazenar e atualizar variáveis locais dentro do componente. 
    
- **Efeitos Colaterais:** Utilizar o `useEffect` para executar operações após a renderização, como chamadas de API ou manipulação do DOM.
    
- **Reutilização de Lógica:** Criar **Hooks customizados** para compartilhar comportamento entre diferentes componentes. 
    

Para funcionar corretamente, os Hooks devem ser chamados **apenas no nível mais alto** do componente (não dentro de loops ou condições) e apenas dentro de componentes funcionais ou outros Hooks customizados.

### Exemplos
``` tsx
// 1) Função JS
const teste = () => {
  return 1 + 1;
}

// 2) Função JS
const useTeste = () => {
  return 1 + 1;
}

// 3) React hook
const useTest = () => {
  const [value] = useState(1 + 1)
  return value;
}

// 4) Função JS que retorna HTML react
const test = () => {
  return (
    <div>Teste</div>
  )
}

// 5) Componente Funcional
const Teste = () => {
  return (
    <div>Teste</div>
  );
}
```

1. Nome não começa com letra maiúscula e não retorna JSX
2. Possui o prefixo use (característica de um hook react), nome não começa com letra maiúscula e não retorna JSX
3. É um hook, pois possui o prefixo use e contém um react hook
4. Não é um componente, pois não começa com letra maiúscula
5. É um componente, pois começa com a letra maiúscula e retorna um JSX

## Contador utilizando useState()
O useState() serve para guardar o estado de uma variável
``` tsx
import { useState } from 'react'

export function App() {
  const [count, setCount] = useState(0)

  return (
    <div>
      <button onClick={() => setCount(count + 1)}>{count}</button>
    </div>
  )
}
```
No exemplo acima, temos o parâmetro 0 no useState que é o valor definido para a renderização inicial este valor é definido como inicialState. O count seria o estado atual. O setCount é a função que altera o estado do count para um outro valor e ativa uma re-renderização.
### Fluxo de Renderização com useState()
Quando o estado é atualizado, ocorre o fluxo de renderização, que é dividido em três etapas:
### 1. Trigger
 - O processo inicia quando a função de atualização do useState é chamada, mas o estado ainda não é atualizado e permanece até o próximo ciclo. 
### 2. Renderização
- O React executa novamente a função do componente. É neste momento que:
	- O useState retorna o novo valor do estado
	- Todo o código do componente é reexecutado para gerar o novo JSX.
	- O React compara o novo JSX com o anterior (Virtual DOM) para calcular as diferenças.
### 3. Commit
- O React aplica as mudanças calculadas no DOM real do navegador, atualizando a interface visual que o usuário vê.
## Listas
Quando utilizar listas no React, é uma boa prática utilizar a propriedade key em elementos `<li>`. A key serve para identificar quais itens foram atualizados, adicionados e removidos durante a reconciliação do Virtual DOM. 
Ao utilizar a key, o React:
- Otimiza a performance, pois atualiza apenas os elementos modificados ao invés de re-renderizar todos os elementos.
- Mantém o estado correto, evitando problemas como a perda de foco em inputs ou comportamento inesperado de componentes quando a ordem dos itens é alterada.
### Exemplo
#### App.tsx
``` tsx
import { useState } from "react";

export function App() {

 const [list, setList] = useState([
  {id: 1, label: 'Fazer café'},
  {id: 2, label: 'Fazer café'},
  {id: 3, label: 'Fazer almoço'},
  {id: 4, label: 'Fazer jantar'}
 ]);

  return (
    <div>
      <input type="text" />
      <button>Adicionar</button>

      <ol>
        {list.map((listItem: {id: number, label: string}) => (
          <li key={listItem.id}>{listItem.label}</li>
        ))}
      </ol>
      
    </div>
  )
}
```
### Adição de itens dinamicamente na lista
#### App.tsx
``` tsx
import { useState } from "react";

export function App() {
 const [value, setValue] = useState('')
 const [list, setList] = useState([
  {id: 1, label: 'Fazer café'},
  {id: 2, label: 'Fazer café'},
  {id: 3, label: 'Fazer almoço'},
  {id: 4, label: 'Fazer jantar'}
 ]);

  return (
    <div>
      <input type="text" value={value} onChange={(e) => setValue(e.target.value)}/>
      <button onClick={() => {
	        setList([...list,{id: (list.length + 1), label: value}])
	        setValue('')
	      }
      }>Adicionar</button>
      <ol>
        {list.map((listItem: {id: number, label: string}) => (
          <li key={listItem.id}>{listItem.label}</li>
        ))}
      </ol>
    </div>
  )
}
```

### Adição de botões concluir e remover
#### App.tsx
``` tsx
import { useState } from "react";

export function App() {
  const [value, setValue] = useState("");
  const [list, setList] = useState([
    { id: 1, label: "Fazer café", completed: false },
    { id: 2, label: "Fazer café", completed: false },
    { id: 3, label: "Fazer almoço", completed: false },
    { id: 4, label: "Fazer jantar", completed: false },
  ]);

  return (
    <div>
      <input
        type="text"
        value={value}
        onChange={(e) => setValue(e.target.value)}
      />
      <button
        onClick={() => {
          setList([
            ...list,
            { id: list.length + 1, label: value, completed: false },
          ]);
          setValue("");
        }}
      >
        Adicionar
      </button>
      <ol>
        {list.map(
          (listItem: { id: number; label: string; completed: boolean }) => (
            <li key={listItem.id}>
              {listItem.label}
              {listItem.completed ? "Concluido" : ""}
              <button
                onClick={() =>
                  setList([
                    ...list.map((item) => ({
                      ...item,
                      completed:
                        item.id === listItem.id ? true : item.completed,
                    })),
                  ])
                }
              >
                Concluir
              </button>
              <button
                onClick={() =>
                  setList([...list.filter((item) => item.id !== listItem.id)])
                }
              >
                Remover
              </button>
            </li>
          ),
        )}
      </ol>
    </div>
  );
}
```
## Properties (Props)
Props são valores passados de um componente pai para um componente React. Elas funcionam de maneira semelhante aos parâmetros de uma função e podem receber qualquer valor válido em JavaScript, como **valores primitivos**, **objetos**, **arrays**, **funções** e **elementos React**.
### Arquivos após componentização
#### App.tsx
```tsx
import { useState } from "react";
import { InputAdd } from "./components/InputAdd";

export function App() {
  const [list, setList] = useState([
    { id: 1, label: "Fazer café", completed: false },
    { id: 2, label: "Fazer café", completed: false },
    { id: 3, label: "Fazer almoço", completed: false },
    { id: 4, label: "Fazer jantar", completed: false },
  ]);

  return (
    <div>
      <InputAdd
        onAdd={(value) => {setList([...list,
          {id: (list.length + 1), completed: false, label: value}])}}
      />

      <ol>
        {list.map(
          (listItem: { id: number; label: string; completed: boolean }) => (
            <li key={listItem.id}>
              {listItem.label}
              {listItem.completed ? "Concluido" : ""}

              <button
                onClick={() =>
                  setList([
                    ...list.map((item) => ({
                      ...item,
                      completed:
                        item.id === listItem.id ? true : item.completed,
                    })),
                  ])
                }
              >
               Concluir
              </button>
              <button
                onClick={() =>
                  setList([...list.filter((item) => item.id !== listItem.id)])
                }
              >
                Remover
              </button>
            </li>
          ),
        )}
      </ol>
    </div>
  );
}
```
#### InputAdd.tsx
```tsx
import { useState } from "react";

interface InputAddProps {
  onAdd(value: string): void;
}

export const InputAdd = (props: InputAddProps) => {
    const [value, setValue] = useState("");
    return (
        <div>
            <input
        type="text"
        value={value}
        onChange={(e) => setValue(e.target.value)}
      />

      <button
        onClick={() => { props.onAdd(value); setValue(""); }}
      >
        Adicionar
      </button>
        </div>
    )
}
```
## Refatorações
#### App.tsx
```tsx
import { useState } from "react";
import { InputAdd } from "./components/InputAdd";

export function App() {
  const [list, setList] = useState([
    { id: 1, label: "Fazer café", completed: false },
    { id: 2, label: "Fazer café", completed: false },
    { id: 3, label: "Fazer almoço", completed: false },
    { id: 4, label: "Fazer jantar", completed: false },
  ]);

  const handleAdd = (value: string) => {
    setList([...list,
          {id: (list.length + 1), completed: false, label: value}])
  }

  return (
    <div>
     <InputAdd onAdd={handleAdd}/>
      <ol>
        {list.map(
          (listItem: { id: number; label: string; completed: boolean }) => (
            <li key={listItem.id}>
              {listItem.label}

              {listItem.completed ? "Concluido" : ""}
              
              <button
                onClick={() =>
                  setList([
                    ...list.map((item) => ({
                      ...item,
                      completed:
                        item.id === listItem.id ? true : item.completed,
                    })),
                  ])
                }
              >
                Concluir
              </button>
              <button
                onClick={() =>
                  setList([...list.filter((item) => item.id !== listItem.id)])
                }
              >
                Remover
              </button>
            </li>
          ),
        )}
      </ol>
    </div>
  );
}
```
#### InputAdd.tsx
```tsx
import { useState } from "react";

interface InputAddProps {
  onAdd(value: string): void;
}

export const InputAdd = (props: InputAddProps) => {
    const [value, setValue] = useState("");
    const handleAdd = () => {
      props.onAdd(value);
      setValue("")
    }

    return (
        <div>
            <input
        type="text"
        value={value}
        onChange={(e) => setValue(e.target.value)}
      />

      <button
        onClick={() => {handleAdd();}}
      >
        Adicionar
      </button>
        </div>
    )
}
```
Adição de event handlers (handleAdd), que são responsáveis por gerenciar e responder as interações dos usuários

## useEffect
O useEffect é um React hook que permite executar efeitos colaterais em componentes. Ele faz chamadas de API, interações com o DOM e *event listening*. Ele pode ser utilizado de 3 maneiras distintas [[useEffect sem argumentos]], [[useEffect com array vazio]] e [[useEffect com array de dependências]]
#### App.tsx
```tsx
import { useState, useEffect } from "react";
import { InputAdd } from "./components/InputAdd";
import { ToDoItem } from "./components/ToDoItem";
import { List } from "./components/List";
import { ToDoAPI, type IToDo } from "./shared/services/api/ToDoAPI";

export function App() {

  const [list, setList] = useState<IToDo[]>([]);

  useEffect(() => {
    ToDoAPI.getAll()
      .then(data => setList(data));
  }, []);

  const handleAdd = (value: string) => {
    ToDoAPI.create({ label: value, completed: false})
    .then(data => setList([...list, data]))
  };

  const handleComplete = (id: number) => {
    ToDoAPI.updateById(id, {completed: true}).then(() => {
      setList([
        ...list.map((item) => ({
          ...item,
          completed: item.id === id ? true : item.completed,
        })),
      ]);
    })
  };


  const handleRemove = (id: number) => {
    
    ToDoAPI.deleteById(id).then(() => {
      setList([...list.filter((item) => item.id !== id)]);

    })
  };

  return (
    <div>
      <InputAdd onAdd={handleAdd} />

      <List>
        {list.map(
          (listItem: { id: number; label: string; completed: boolean }) => (
            <ToDoItem
              key={listItem.id}
              id={listItem.id}
              label={listItem.label}
              completed={listItem.completed}
              onComplete={() => handleComplete(listItem.id)}
              onRemove={() => handleRemove(listItem.id)}
            />
          ),
        )}
      </List>
    </div>
  );
}

```
#### server.ts
```tsx
import { createServer, Model } from 'miragejs'

createServer({
    models: {
        toDos: Model
    },
    seeds(server){
        const toDosAsString = localStorage.getItem('MOCK_TODOS');
        if(toDosAsString === null) return;

        const toDos = JSON.parse(toDosAsString);
        console.log(toDos)

        toDos.models.forEach((toDo: {}) => server.schema.create('toDos', toDo))
    },
    routes() {
        this.namespace = 'api';

        this.get('/toDos', () => {
            return this.schema.all('toDos');
        });

        this.post('/toDos', (schema, request) => {
            const attrs = JSON.parse(request.requestBody);

            const toDo = schema.create('toDos', attrs);

            const toDos = schema.all("toDos");
            localStorage.setItem('MOCK_TODOS', JSON.stringify(toDos))

            return toDo;
        });

        this.delete('/toDos/:id',(schema, request) => {
            const id = request.params.id;
            
            const toDo = schema.find('toDos', id);
            toDo?.destroy()

            const toDos = schema.all("toDos");
            localStorage.setItem('MOCK_TODOS', JSON.stringify(toDos))

            return {}
        });

        this.put('/toDos/:id', (schema, request) => {
            const id = request.params.id;

            const newAttrs = JSON.parse(request.requestBody)

            const toDo = schema.find('toDos', id)
            toDo?.update(newAttrs)

            const toDos = schema.all("toDos");
            localStorage.setItem('MOCK_TODOS', JSON.stringify(toDos))

            return {}
        })
    },

})
```

## Estilização
A estilização em React pode ser diferente do CSS tradicional porque o uso de CSS global pode gerar conflitos em aplicações baseadas em componentes reutilizáveis. Uma boa prática para evitar esse problema é utilizar CSS Modules, que escopam os estilos a componentes específicos, reduzindo colisões entre classes CSS.
### Exemplos
Na imagem a seguir, temos um exemplo de componente com CSS Module correspondente
![[ImagemComponenteComCssModule.png|274]]
Abaixo estão os blocos de código correspondentes aos arquivos da imagem
#### InputAdd.module.css
```css
.Container {
  gap: 16px;
  padding: 8px;
  display: flex;
}

.Input {
  flex: 1;
  padding: 8px;
  font-size: 16px;
  border: 1px solid #00000025;
  border-radius: 4px;
  padding-left: 16px;
  padding-right: 16px;
}

.Button {
  border: none;
  padding: 8px;
  color: white;
  cursor: pointer;
  font-size: 16px;
  border-radius: 4px;
  padding-left: 16px;
  padding-right: 16px;
  background: linear-gradient(90deg, #2e8b57, #3cb371);
}

.Button:hover {
  background: linear-gradient(90deg, #34985f, #43cd81);
}

.Button:active {
  background: linear-gradient(90deg, #3a8d5e, #4cb27a);
}
```
#### InputAdd.tsx
```tsx
import { useState } from "react";
import InputAddStyles from "./InputAdd.module.css"

interface InputAddProps {
  onAdd(value: string): void;
}

export const InputAdd = (props: InputAddProps) => {
  const [value, setValue] = useState("");

  const handleAdd = () => {
    props.onAdd(value);
    setValue("");
  };

  return (
    <div className={InputAddStyles.Container}>
      <input
        value={value}
        className={InputAddStyles.Input}
        onChange={(e) => setValue(e.target.value)}
      />
      <button onClick={handleAdd} className={InputAddStyles.Button}>Adicionar</button>
    </div>
  );
};
```
## Routing
A seguir, vamos adicionar rotas para as páginas da aplicação utilizando a biblioteca **React Router**. As rotas serão a Página Inicial e a página Sobre.
### Códigos
#### About.tsx
```tsx
import { PageLayout } from "../shared/layout/page-layout/PageLayout"

export const About = () => {


    return (
        <div>
            <PageLayout title="Sobre" >
            <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Itaque similique at minus ratione harum repellat molestias ut quam id repellendus?</p>
            <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Itaque similique at minus ratione harum repellat molestias ut quam id repellendus?</p>
            <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Itaque similique at minus ratione harum repellat molestias ut quam id repellendus?</p>
            </PageLayout>
        </div>
    )
}
```
#### Home.tsx
```tsx
import { useEffect, useState } from "react";
import { ToDoAPI, type IToDo } from "../shared/services/api/ToDoAPI";
import { InputAdd } from "../components/InputAdd";
import { List } from "../components/List";
import { ToDoItem } from "../components/ToDoItem";
import { PageLayout } from "../shared/layout/page-layout/PageLayout";


export const Home = () => {
   const [list, setList] = useState<IToDo[]>([]);
   
     useEffect(() => {
       ToDoAPI.getAll()
         .then(data => setList(data));
     }, []);
   
     const handleAdd = (value: string) => {
   
       ToDoAPI.create({ label: value, completed: false})
       .then(data => setList([...list, data]))
     };
   
     const handleComplete = (id: number) => {
       ToDoAPI.updateById(id, {completed: true}).then(() => {
         setList([
           ...list.map((item) => ({
             ...item,
             completed: item.id === id ? true : item.completed,
           })),
         ]);
   
       })
   
     };
   
   
     const handleRemove = (id: number) => {
       
       ToDoAPI.deleteById(id).then(() => {
         setList([...list.filter((item) => item.id !== id)]);
   
       })
     };
   
     return (
       <PageLayout title="TODO List">
         <InputAdd onAdd={handleAdd} />
   
         <List>
           {list.map(
             (listItem: { id: number; label: string; completed: boolean }) => (
               <ToDoItem
                 key={listItem.id}
                 id={listItem.id}
                 label={listItem.label}
                 completed={listItem.completed}
                 onComplete={() => handleComplete(listItem.id)}
                 onRemove={() => handleRemove(listItem.id)}
               />
             ),
           )}
         </List>
       </PageLayout>
     );
    
};
```
#### App.tsx
As modificações são feitas no componente principal, o App
```tsx 
import { BrowserRouter, Navigate, Route, Routes } from "react-router";

import { About } from "./pages/About";
import { Home } from "./pages/Home";
import { AppLayout } from "./shared/layout/AppLayout";

export function App() {

  return (
    <BrowserRouter>
      <AppLayout>
        
        <Routes>
          <Route path='/' element={<Home />}/>
          <Route path="/sobre" element={<About />}/>

		//Este tratamento é feito para o caso do usuário digitar uma rota inexistente.
          <Route path="*" element={<Navigate to='/'/>}/>
        </Routes>
        
      </AppLayout>
    </BrowserRouter>
  )
}

```

### Imagens
Fica assim:
#### Página Inicial
![[ImagemPáginaInicial.png]]
#### Sobre
![[ImagemPáginaSobre.png]]
## Aplicando o Context
Na aplicação, o [[Context]] foi utilizado para autenticação do usuário.

## useCallback e useMemo

## Links
Código do projeto de Lista: https://github.com/jungabriel56/react-curso-inicial