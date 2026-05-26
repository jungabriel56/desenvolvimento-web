**JSX** é uma extensão de sintaxe para JavaScript que permite escrever markup semelhante a HTML dentro de arquivos JavaScript, enquanto **HTML** é a linguagem de marcação padrão usada nativamente pelos navegadores para estruturar páginas web.
### Atributos
- Uma das principais diferenças entre JSX e HTML é que os atributos devem ser escritos de maneira diferente (Ex. class em JSX é className). 
### Fechamento de Tags
- Outra diferença é o fechamento das tags, que se torna obrigatória no JSX (ex: `<img />` em vez de `<img>`).
### Expressões Dinâmicas
-  O JSX permite a inserção de expressões e variáveis JavaScript diretamente no markup usando chaves `{ }`, algo que o HTML puro não suporta nativamente.
### Processamento
- O navegador não entende JSX diretamente; ele precisa ser compilado (transpilado) para chamadas de função JavaScript (como `React.createElement`) por ferramentas como o Babel. O HTML é interpretado diretamente pelo motor de renderização do navegador
### Fragments
- Para retornar múltiplos elementos raiz sem adicionar um `<div>` extra, o JSX utiliza Fragments (`<> ... </>`), enquanto o HTML tradicional requer um elemento pai.