# Conversão de DP Top-down para Bottom-up

Durante o treino no tópico de Programação Dinâmica, com o aumento do nível de dificuldade dos problemas vemos uma tendência de soluções com DP projetadas *Bottom up* ganhando mais relevância, seja por ser amigável a otimizações, ou por ter *constantes* menores. 
Porém, para maratonistas inexperientes projetar uma DP *bottom up* pode não ser uma tarefa fácil ~~e as vezes nada intuitivo~~, e tendem a se agarrar à implementação top-down, o que pode desacelerar seu ritmo de aprendizado.

> Para saber mais sobre as diferenças entre projetar DP de forma top-down ou bottom-up, acompanhe o nosso projeto, em breve teremos um artigo tratando deste assunto!



/* Conversão DP top-down => DP bottom up
//1º passo - construir casos bases <=> base da recursão
//2º passo - definir ordem para calcular estados <=> ordem que vai percorrer a matriz
//(dica: se estiver difícil, desenha uma tabela, e faz setinha pra representar as dependências do que tem que estar calculado antes)
//3º passo - copia e cola as transições do top-down pro bottom-up
//4º passo - troca chamada recursiva pelo acesso do estado na tabela
//5º passo - guardar a resposta calculada
//
//Vantagens:
//Amigável à otimizações (transparente, tem a visão do todo)
//Sem overhead de trocad de context de funções (geralmente mais rápido)
//Consome menos memória (não usa a stack)
//
//Desvatagens:
//Calcula todos os estados (mas na prática ainda é mais rápido que top down na maioria dos problemas)
//Menos intuitivo (dica: não tentar entender soluções a partir de DP bottom-up)