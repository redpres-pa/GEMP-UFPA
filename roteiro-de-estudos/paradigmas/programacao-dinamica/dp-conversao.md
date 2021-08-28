# Conversão de DP Top-down para Bottom-up

Durante o treino no tópico de Programação Dinâmica, com o aumento do nível de dificuldade dos problemas vemos uma tendência de soluções com DP projetadas *Bottom up* ganhando mais relevância, seja por ser amigável a otimizações, ou por ter *constantes* menores. 
Porém, para maratonistas inexperientes projetar uma DP bottom up pode não ser uma tarefa fácil ~~e as vezes nada intuitivo~~, e tendem a se agarrar à implementação top-down, o que pode desacelerar seu ritmo de aprendizado.

> Para saber mais sobre as diferenças entre projetar DP de forma top-down ou bottom-up, acompanhe nosso projeto, em breve teremos um artigo tratando deste assunto!

Bom, embora pensar direto numa implementação bottom up possa ser um pouco dificíl de primeira, converter uma DP top down para bottom up é fácil. Então temos a seguinte estratégia para implementar DP bottom up: Começar implementando top down, e depois converter de top down para bottom up.

<p align="center">
  <img width="350" src="/images/panorama-dp.png">
</p>

O objetivo deste texto então é apresentar um passo a passo para o leitor que ainda não se sente tão confortável em projetar Programação Dinâmica bottom up diretamente, para que continuem melhorando ainda mais suas habilidades enquanto vão aprofundando seu entendimento ao resolver mais problemas e discutir com a comunidade.

## Tabela de Conteúdos

- Passo 0: Fazer uma DP top down
- Passo 1: Construir casos bases
- Passo 2: definir ordem de iteração dos laços
- Passo 3: Copiar as transições da top down
- Passo 4: Trocar chamadas recursivas por acessos à tabela
- Passo 5: Guardar a resposta calculada

## Passo 0: Fazer uma DP Top down

Bem, se você quer converter sua solução de top down para bottom up, você precisa já ter uma solução para o problema que está tentando resolver. 
Se você não sabe como fazer uma solução top down ainda, pode dar uma olhada na referência [1] do nosso [RoadMap](./dp-roadmap.md) de programação dinâmica ou pedir mais orientações para a comunidade. 
A partir daqui assumiremos que o leitor conhece os conceitos de programação dinâmica.

Para que este passo a passo faça mais sentido, iremos trabalhar um exemplo ao longo da discussão. Iremos resolver o problema [Dice Combinatinons](https://cses.fi/problemset/task/1633) do online judge [CSES](https://cses.fi/problemset/).

> Se você ainda não resolveu este problema, pare e tente antes de continuar.

O enunciado do problema pede para acharmos de quantas formas podemos fazer uma soma *n* jogando dados, que tem faces numeradas de 1 a 6.

Ao pedir "**de quantas formas** podemos fazer uma soma" podemos identificar uma natureza combinatória neste problema, visto que queremos *contar* esses jeitos de fazer a soma. 
Então para resolvê-lo vamos usar **análise combinatória**. 

Para cada lançamento do dado você pode obter resultados de 1 a 6, e como cada possibilidade representa uma *forma distinta* (ou um *evento disjunto* em combinatória) de fazer a soma *n*, pelo **princípio da adição**, a resposta de *quantas formas* há de fazer soma *n* é a soma de:

- todas as formas de fazer a soma *n-1*, e tirar 1 no dado para obter soma n-1 + 1 = n.
- todas as formas de fazer a soma *n-2*, e tirar 2 no dado para obter soma n-2 + 2 = n.
- todas as formas de fazer a soma *n-3*, e tirar 3 no dado para obter soma n-3 + 3 = n.
- todas as formas de fazer a soma *n-4*, e tirar 4 no dado para obter soma n-4 + 4 = n.
- todas as formas de fazer a soma *n-5*, e tirar 5 no dado para obter soma n-5 + 5 = n.
- todas as formas de fazer a soma *n-6*, e tirar 6 no dado para obter soma n-6 + 6 = n.

Dessa forma vemos uma relação entre a resposta de quantas formas há de fazer soma *n* a partir de quantas formas há de fazer somas *n-1*, *n-2*, *n-3*, *n-4*, *n-5* e *n-6*. Mais especificamente, se criarmos uma função f(n) que significa "de quantas formas podemos obter soma n lançando dados de 6 faces", temos a seguinte relação *recursiva*:

```
f(n) = f(n-1) + f(n-2) + f(n-3) + f(n-4) + f(n-5) + f(n-6)
```

> Esse é um bom momento para observar que o problema que queremos resolver tem a propriedade de **subestrutura ótima**, dado que a resposta para o nosso problema depende da resposta de subproblemas mais simples.






## Passo 1: Construir casos bases (TODO)




/* comentários Conversão DP top-down => DP bottom up


//1º passo - construir casos bases <=> base da recursão

//2º passo - definir ordem para calcular estados <=> ordem que vai percorrer a matriz

//(dica: se estiver difícil, desenha uma tabela, e faz setinha pra representar as dependências do que tem que estar calculado antes)

//3º passo - copia e cola as transições do top-down pro bottom-up

//4º passo - troca chamada recursiva pelo acesso do estado na tabela

//5º passo - guardar a resposta calculada

> Autor: Felipe Cardoso