Ao utilizar o useEffect sem argumentos, ele será executado a cada renderização do componente. Por isso, é necessário atenção, pois ele pode gerar loops infinitos.
### Exemplo
```tsx
useEffect(() => {  
	console.log("E aí, isso aqui roda sempre que o componente renderizar!");  
});
```
