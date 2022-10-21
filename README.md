# type-annotations-advantages

# Por que devemos usar type annotations?

Quantas horas você gastou depurando por causa da tipagem dinâmica?

À medida que os contribuidores crescem e o código está sendo aproximado do nível de produção, não ter digitação estática ou verificação de tipo pode levar a surpresas desagradáveis.

Este foi um sentimento compartilhado entre muitos no ecossistema Python. No entanto, manter a liberdade permitida pela tipagem dinâmica, mas mitigar seu impacto negativo, é difícil.

- Use type annotations!!!

Se há um recurso em Python que maximiza o impacto positivo em seu código, exigindo o mínimo de esforço, são os type annotatios.

Ele permite que o desenvolvedor comunique efetivamente os tipos de argumentos esperados e os valores de retorno com o interpretador (e outros desenvolvedores também), mantendo as vantagens da tipagem dinâmica.

# Digitação dinâmica em Python

Então, afinal, o que é dynamic typing (tipagem dinâmica)? # Show me the code!

![image](https://user-images.githubusercontent.com/107052041/197237348-16565792-648a-4f46-817e-7176b9d1c669.png)


Nos bastidores, variáveis ​​em Python como a acima são ponteiros, apontando para objetos com um determinado tipo.
No entanto, os ponteiros não se restringem a representar objetos de tipo fixo para um determinado nome. 
Isso nos dá muita liberdade. Por exemplo, funções podem aceitar qualquer tipo como argumento, pois em segundo plano, um ponteiro é passado.

Infelizmente, sem os devidos cuidados, isso pode dar me..   muito errado!

"dynamic typing" és una "faca de dois legumes"

Basta pensar no exemplo a seguir.

![image](https://user-images.githubusercontent.com/107052041/197237805-458a8d63-9717-4d15-8bd2-10767b2ce4da.png)

Esta simples função de gerar estatística também funciona para listas e matrizes NumPy! Bacana!

Bem... não totalmente, pois há muitas maneiras de se queimar com isso.
Por exemplo, você pode passar involuntariamente algo que faz com que a função quebre. Isso é o que acontece se chamarmos a função com uma string.

![image](https://user-images.githubusercontent.com/107052041/197238128-e535c56a-338f-4213-af27-fc0cf6341f2d.png)

O operador de divisão não está definido entre strings e inteiros, daí o erro. Como o Python é uma linguagem interpretada, esse problema não surgiria até que a função fosse realmente chamada com um argumento incorreto. Isso pode ocorrer após semanas de tempo de execução. Linguagens como C podem detectar esses erros em tempo de compilação antes que algo dê errado.

As coisas podem ficar ainda piores. Por exemplo, vamos chamar a função com um dicionário.

![image](https://user-images.githubusercontent.com/107052041/197238233-131981cf-d5e8-4ab4-8c1d-3adb3235ea62.png)


A execução é bem sucedida, mas o resultado está errado. Quando um dicionário é passado as funções min e max calculam o mínimo e o máximo das chaves, não os valores que queremos!
Esse tipo de bug pode permanecer sem ser detectado por um longo tempo, enquanto isso, você fica com a impressão de que as coisas estão bem.

Vamos ver o que podemos fazer para evitar problemas como esses!

# Insira function annotations ( anotações de função ) e type hints ( dicas de tipos )

Em 2006, o PEP 3107 introduziu anotações de função, que foram estendidas no PEP 484 com dicas de tipo. (PEP é a abreviação de Python Enhancement Proposal, que é a maneira do Python de sugerir e discutir novos recursos de linguagem.)

A anotação de função é simplesmente “uma sintaxe para adicionar anotações de metadados arbitrárias a funções Python”, como afirma o PEP 3107. 
- Como fica na prática?

![image](https://user-images.githubusercontent.com/107052041/197238263-0ab94550-cce2-4707-8a77-0354587a12eb.png)


Os tipos podem ser sugeridos com o argumento: type = default_value e valores de retorno com def function(...) -> type.

Estas não são aplicadas e ignoradas pelo interpretados. No entanto, isso não significa que eles não sejam incrivelmente úteis! 
Para convencê-lo, vamos ver o que podemos ganhar!

# Desenvolvimento mais rápido com a auto-completação de código!

Você já tentou desenvolver em um editor de texto barebones como o Bloco de Notas?
Você tem que digitar tudo e ter em mente o que é o que o tempo todo. 
Mesmo um IDE não pode ajudá-lo se não tiver ideia sobre o objeto que você está usando.

Dê uma olhada no exemplo abaixo.
Autocompletar no PyCharm:

![image](https://user-images.githubusercontent.com/107052041/197240336-264ef828-deb9-4f62-bc8f-fa0868330f83.png)


Com a anotação de função, o IDE está ciente do tipo do objeto de dados, que é o valor de retorno da função preprocess_data. 
Assim, você obtém o preenchimento automático, o que economiza muito tempo.

Isso também ajuda ao usar a função. Na maioria das vezes, a definição está em um módulo totalmente diferente, longe de onde você está chamando. 
Ao informar ao IDE o tipo de argumentos, ele poderá ajudá-lo a passar os argumentos no formato correto sem precisar verificar manualmente a documentação ou a implementação.


Os desenvolvedores gastam muito mais tempo lendo código do que escrevendo. Eu acredito que um ótimo código, é um código auto-documentado. 

Com estrutura adequada e nomenclatura de variáveis, raramente são necessários comentários. 
A Function Annotation (anotação de função) contribui significativamente para isso.
Apenas uma olhada na definição revelará muito sobre como usá-la.

- Type Checking ( verificação de tipo )

As anotações são acessíveis do lado de fora da função.

![image](https://user-images.githubusercontent.com/107052041/197238969-9d7df894-efe3-4ce1-b918-e53791dc9612.png)


Isso não é útil apenas para o programador, mas também para o próprio programa! 
Antes de chamar a função, você pode verificar a validade de seus argumentos em tempo de execução, se necessário.


Com base no PEP 484, a verificação de tipo foi levada para o próximo nível!!

Ele incluía o módulo de digitação, “fornecendo uma sintaxe padrão para anotações de tipo, abrindo o código Python para facilitar a análise estática e refatoração, verificação de tipo de tempo de execução potencial e (talvez, em alguns contextos) geração de código utilizando informações de tipo”, conforme declarado no PEP.

Para dar um exemplo mais concreto, o módulo de digitação contém List, então usando a anotação List[int], você pode dizer que a função espera (ou retorna) uma lista de inteiros.

- Um passo adiante: validação de dados com pydantic

A verificação de tipos abre muitas oportunidades. No entanto, fazê-lo manualmente o tempo todo não é tão conveniente.

Se você deseja uma solução estável, tente o pydantic, uma biblioteca de validação de dados. Usando sua classe BaseModel, você pode validar dados em tempo de execução.

![image](https://user-images.githubusercontent.com/107052041/197247155-9720ab07-434a-429f-9120-cc9a918a67d4.png)

Você pode ir além deste exemplo  fornecendo validadores personalizados para modelos pydantic.

pydantic é um dos pilares do FastAPI, (baseado no Openapi) que é um dos frameworks de desenvolvimento web em Python.

Lá, o pydantic disponibiliza para definir facilmente os esquemas JSON para os endpoints.



# Então, espero ter te convencido!

As Type Annotations (anotações de tipo) exigem um esforço mínimo, mas têm um enorme impacto positivo em seu código:
    • torna o código mais fácil de ler para você e sua equipe,
    • incentiva você a ter tipos em mente,
    • ajuda a identificar problemas relacionados ao tipo,
    • permite a verificação de tipo adequada.
    
Se você ainda não está usando, você deve começar a fazê-lo agora! 

Esta é uma das maiores melhorias de código que você pode fazer com apenas uma pequena quantidade de trabalho!





