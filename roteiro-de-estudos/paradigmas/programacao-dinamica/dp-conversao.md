# Conversão de DP Top-down para Bottom-up

Durante o treino no tópico de Programação Dinâmica, com o aumento do nível de dificuldade dos problemas vemos uma tendência de soluções com DP projetadas *Bottom up* ganhando mais relevância, seja por ser amigável a otimizações, ou por ter *constantes* menores. 
Porém, para maratonistas inexperientes projetar uma DP bottom up pode não ser uma tarefa fácil ~~e as vezes nada intuitivo~~, e tendem a se agarrar à implementação top-down, o que pode desacelerar seu ritmo de aprendizado.

> Para saber mais sobre as diferenças entre projetar DP de forma top-down ou bottom-up, acompanhe nosso projeto, em breve teremos um artigo tratando deste assunto!

Bom, embora pensar direto numa implementação bottom up possa ser um pouco dificíl de primeira, converter uma DP top down para bottom up é fácil. Então temos a seguinte estratégia para implementar DP bottom up: Começar implementando top down, e depois converter de top down para bottom up.

<p align="center">
  <img width="350" src="images/panorama-dp.png">
</p>

O objetivo deste texto então é apresentar um passo a passo para o leitor que ainda não se sente tão confortável em projetar Programação Dinâmica bottom up diretamente, para que continuem melhorando ainda mais suas habilidades enquanto vão aprofundando seu entendimento ao resolver mais problemas e discutir com a comunidade.

## Tabela de Conteúdos (TODO)


/* Conversão DP top-down => DP bottom up


//1º passo - construir casos bases <=> base da recursão

//2º passo - definir ordem para calcular estados <=> ordem que vai percorrer a matriz

//(dica: se estiver difícil, desenha uma tabela, e faz setinha pra representar as dependências do que tem que estar calculado antes)

//3º passo - copia e cola as transições do top-down pro bottom-up

//4º passo - troca chamada recursiva pelo acesso do estado na tabela

//5º passo - guardar a resposta calculada

> Autor: Felipe Cardoso