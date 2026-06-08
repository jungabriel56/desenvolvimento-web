Quando o useEffect é utilizado com um array de dependências, ele é executado após a primeira renderização e novamente sempre que uma das dependências mudar. Isso permite controlar quando um efeito colateral deve ser executado, evitando execuções desnecessárias.
### Exemplo
```tsx
const [nome, setNome] = useState('');
useEffect(() => {
    console.log("E aí! Esse efeito vai rodar toda vez que o 'nome' mudar!");
}, [nome]);
```