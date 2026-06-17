No react, o **Context** é uma maneira de prover dados entre vários componentes sem que seja necessário criar props em cada nível da árvore. 
O **Context** é utilizado quando uma propriedade deve ser utilizada globalmente, como: 
- usuário autenticado;
- tema claro/escuro;
- idioma;
- carrinho de compras;
- configurações da aplicação.
A utilização global do **Context**, é uma boa prática para evitar o **prop drilling**, que é a repetição de uma propriedade em vários componentes