# type-annotations-advantages
Por que devemos usar type annotations?

Quantas horas você gastou depurando por causa da tipagem dinâmica?

Quando eu comecei com Python, eu vinha de um background em C. Eu não tinha experiência extensa em desenvolvimento de software naquela época, e o gosto da liberdade proporcionado pela digitação dinâmica era boa. Funções que alavancam o polimorfismo e a tipagem permitiram fazer muito com pouco.

Mais tarde, à medida que minha experiência crescia e me envolvia em projetos de grande escala, percebi que essa liberdade é uma bênção maldita. 
À medida que os contribuidores crescem e o código está sendo aproximado do nível de produção, não ter digitação estática ou verificação de tipo pode levar a surpresas desagradáveis.

Este foi um sentimento compartilhado entre muitos no ecossistema Python. No entanto, manter a liberdade permitida pela tipagem dinâmica, mas mitigar seu impacto negativo, é difícil.

Use type annotations!!!

Se há um recurso em Python que maximiza o impacto positivo em seu código, exigindo o mínimo de esforço, são os type annotatios.
Ele permite que o desenvolvedor comunique efetivamente os tipos de argumentos esperados e os valores de retorno com o interpretador (e outros desenvolvedores também), mantendo as vantagens da tipagem dinâmica.

# Digitação dinâmica em Python

Então, afinal, o que é tipagem dinâmica? Show me the code...

![image](https://user-images.githubusercontent.com/107052041/197237348-16565792-648a-4f46-817e-7176b9d1c669.png)


Nos bastidores, variáveis ​​em Python como a acima são ponteiros, apontando para objetos com um determinado tipo. No entanto, os ponteiros não se restringem a representar objetos de tipo fixo para um determinado nome. Isso nos dá muita liberdade. Por exemplo, funções podem aceitar qualquer tipo como argumento, pois em segundo plano, um ponteiro é passado.

Infelizmente, sem os devidos cuidados, isso pode dar errado muito rápido.
A digitação dinâmica é uma faca de dois gumes

Basta pensar no exemplo a seguir.

Esta função estatística simples também funciona para listas e matrizes NumPy! Que incrível!

Bem, não inteiramente. Há muitas maneiras de se queimar com isso. Por exemplo, você pode passar involuntariamente algo que faz com que a função falhe. Isso é o que acontece se chamarmos a função com uma string.

O operador de divisão não está definido entre strings e inteiros, daí o erro. Como o Python é uma linguagem interpretada, esse problema não surgiria até que a função fosse realmente chamada com um argumento incorreto. Isso pode ocorrer após semanas de tempo de execução. Linguagens como C podem detectar esses erros em tempo de compilação antes que algo dê errado.

As coisas podem ficar ainda piores. Por exemplo, vamos chamar a função com um dicionário.

A execução é bem sucedida, mas o resultado está errado. Quando um dicionário é passado, as funções min e max calculam o mínimo e o máximo das chaves, não os valores que queremos. Esse tipo de bug pode permanecer sem ser detectado por um longo tempo, enquanto isso, você fica com a impressão de que as coisas estão bem.

Vamos ver o que podemos fazer para evitar problemas como esses!
Insira anotações de função e digite dicas

Em 2006, o PEP 3107 introduziu anotações de função, que foram estendidas no PEP 484 com dicas de tipo. (PEP é a abreviação de Python Enhancement Proposal, que é a maneira do Python de sugerir e discutir novos recursos de linguagem.)

A anotação de função é simplesmente “uma sintaxe para adicionar anotações de metadados arbitrárias a funções Python”, como afirma o PEP 3107. Como fica na prática?

Os tipos podem ser sugeridos com o argumento: type = default_value e valores de retorno com def function(...) -> type.

Estas não são aplicadas e ignoradas pelo intérprete. No entanto, isso não significa que eles não sejam incrivelmente úteis! Para convencê-lo, vamos ver o que podemos ganhar!
Desenvolvimento mais rápido com conclusão de código

Você já tentou desenvolver em um editor de texto barebones como o Bloco de Notas? Você tem que digitar tudo e ter em mente o que é o que o tempo todo. Mesmo um IDE não pode ajudá-lo se não tiver ideia sobre o objeto que você está usando.

Dê uma olhada no exemplo abaixo.
Autocompletar no PyCharm

Com a anotação de função, o IDE está ciente do tipo do objeto de dados, que é o valor de retorno da função preprocess_data. Assim, você obtém o preenchimento automático, o que economiza muito tempo.

Isso também ajuda ao usar a função. Na maioria das vezes, a definição está em um módulo totalmente diferente, longe de onde você está chamando. Ao informar ao IDE o tipo de argumentos, ele poderá ajudá-lo a passar os argumentos no formato correto sem precisar verificar manualmente a documentação ou a implementação.
Codifique como documentação

Os desenvolvedores gastam muito mais tempo lendo código do que escrevendo. Eu acredito firmemente que um ótimo código é auto-documentado. 
Com estrutura adequada e nomenclatura de variáveis, raramente são necessários comentários. A Function Annotation (anotação de função) contribui significativamente para isso. Apenas uma olhada na definição revelará muito sobre como usá-la.
Verificação de tipo

As anotações são acessíveis do lado de fora da função.

Isso não é útil apenas para o programador, mas também para o próprio programa! Antes de chamar a função, você pode verificar o




