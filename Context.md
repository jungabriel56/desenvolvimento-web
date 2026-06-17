No React, o **Context** é uma maneira de disponibilizar dados para componentes descendentes sem que seja necessário passar [[React#Properties (Props)|props]] explicitamente por todos os níveis intermediários da árvore.

Ele pode ser utilizado quando vários componentes precisam acessar informações compartilhadas, como:
- usuário autenticado;
- tema claro ou escuro;
- idioma;
- carrinho de compras;
- configurações da aplicação.

O **Context** pode ajudar a evitar o **prop drilling**, que ocorre quando uma prop precisa atravessar vários componentes intermediários apenas para chegar ao componente que realmente a utiliza.

Entretanto, o **Context** não deve ser utilizado globalmente por padrão. Para dados utilizados por componentes próximos, o uso de props geralmente continua sendo a solução mais simples e explícita.