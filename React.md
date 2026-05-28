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

## Exemplos

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