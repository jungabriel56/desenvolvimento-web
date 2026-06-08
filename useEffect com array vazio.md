Quando o useEffect é utilizado com um array vazio como dependência, ele é executado após a montagem do componente, ou seja, após a primeira renderização. Em produção, esse efeito normalmente roda uma vez durante a montagem.
### Exemplo
```tsx
useEffect(() => {
	console.log("Sou executado apenas na montagem do componente! Tipo um componentDidMount");
})
```
