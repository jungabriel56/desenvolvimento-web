Quado o useEffect é utilizado com dependências, ele será executado toda vez que um dos valores passados mudar. Isso é utilizado para melhorar o desempenho da aplicação, de modo que uma ação seja executada apenas quando for necessário.
### Exemplo
```tsx
const [nome, setNome] = useState('');
useEffect(() => {
    console.log("E aí! Esse efeito vai rodar toda vez que o 'nome' mudar!");
}, [nome]);
```