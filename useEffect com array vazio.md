Quando o useEffect é utilizado com um array vazio como parâmetro, ele é executado apenas na montagem do componente. Ou seja, apenas na primeira vez que o componente for renderizado.
### Exemplo
```tsx
useEffect(() => {
	console.log("Sou executado apenas na montagem do componente! Tipo um componentDidMount");
})
```
