São props que contêm lógica executável ou elementos React, permitindo comunicação de filho para pai (callbacks) ou injeção dinâmica de UI.

- **Exemplos:** `function` (callbacks), `element` (componentes JSX), `node` (qualquer coisa renderizável). 
    
- **Uso:** Manipuladores de eventos (ex: `onClick`), renderização de componentes filhos (`children`), ou lógica personalizada. 
    
- **Validação:** `PropTypes.func`, `PropTypes.element`, `PropTypes.node`.
    

> **Nota Importante:** Com a adoção crescente de **TypeScript** no ecossistema React, essa validação runtime (`prop-types`) tem sido substituída por tipagem estática em tempo de compilação (interfaces e types), que oferece maior segurança e autocompletar no editor de código.