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

```
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
```
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

Quando o estado é atualizado, é realizado o fluxo de renderização, que é dividido em t

