# RoadMap de Programação Dinâmica
Este documento contém algumas das principais referências usadas como leitura complementar ao treino feito no GEMP, no tópico de Programação Dinâmica.

> Durante o texto por DP (Dynamic Programming) leia-se Programação Dinâmica.

A ordem recomendada de leitura foi organizada de forma a trabalhar os aspectos de programação dinâmica em ordem crescente de dificuldade, como complemento a um treino orientado a resolução de problemas. Os principais Online Judges para praticar Programação Dinâmica são o [CSES](https://cses.fi/problemset/list/) e o [AtCoder](https://atcoder.jp/contests/dp/tasks).

Os passos que tomamos durante o treino em Programação Dinâmica são os seguintes:

1. Melhorar soluções recursivas (backtracing) com memoization, servindo de introdução à DPs top down.
2. Estudar os principais conceitos de Programação Dinâmica, como, estados, subproblemas, transições, subestrutura ótima, sobreposição de subproblemas, etc.
3. Estudar as formas de projetar DP, *top down* e *bottom up*, e como converter facilmentre entre os dois tipos.
4. Estudar como implementar DPs bottom up eficientemente ao levar em consideração alguns tópicos de arqutetura de computadores, como memória cache, *branching* etc.
5. Estudar os estilos de implementação de DP, *backward* e *forward*, vantagens e desvantagens. 
6. Otimizar soluções com DP, de forma a melhorar a complexidade temporal e/ou espacial dos algoritmos, que recaem em otimizações "estruturais" ou "matemáticas".

> OBS: Uma experiência completa no treino de Programação Dinâmica para programação competitiva não é puramente teória, mas também leva em conta a prática, resolvendo problemas, e as discussões feitas com a comunidade. Logo, as referências nesse documento são puramente complementares.


## Comentários sobre as referências
- Em [1] temos uma discussão sobre otimizações de soluções recursivas, que introduz DP top down. PS: Aonde ele diz "optimal subproblems" era pra ser "Overlapping subproblems".
- Em [2] temos um tutorial para quem está começando. Pode ser lido até a seção "intermediate", que contém exemplos mais simples.
- Em [3] Vemos uma discussão sobre *top down* vs *bottom up*, com alguns comentários interessantes. O leitor pode dar uma passada neles e ver os que mais o agradam, mas eu dou destaque para os comentários do Gassa e do ko_osaga, que mostram os dois lados da discussão.
- Em [4] tem uma discussão sobre paralelização de DP, mas o leitor pode filtrar o conteúdo. A parte da discussão em cima de dp é uma boa leitura complementar, além de que o autor dá vários exemplos passo a passo de como fazer dp. Nesses exemplos o leitor pode ler até os passos 6, caso paralelização não seja de interesse.
- Em [5] o autor estende a discussão feita em [2], e continua discutindo vários aspectos de dp com vários exemplos. Bem, é uma longa discussão. A princípio eu recomendaria ler até a seção "Forward vs backward DP style", mas a próxima, de recuperar a solução pode ser uma boa, já que é uma tarefa bem comum em problemas de DP. Depois daí ele começa a falar de otimizações, e essa parte é importante porém opcional num primeiro momento.

**Ordem recomendada de leitura:** [1] -> [2] -> [3] -> [4] -> [5]

## Referências

[1] [Use Dynamic Programming to Improve Recursive Solutions](https://medium.com/@verdi/use-dynamic-programming-to-improve-recursive-solutions-493358b9c35)

[2] [DYNAMIC PROGRAMMING: FROM NOVICE TO ADVANCED](https://www.topcoder.com/thrive/articles/Dynamic%20Programming:%20From%20Novice%20to%20Advanced)

[3] [Why do top guys favor array-based versus recursive DP?](https://codeforces.com/blog/entry/44356)

[4] [Dynamic Programming Pattern](https://patterns.eecs.berkeley.edu/?page_id=416)

[5] [Everything About Dynamic Programming](https://codeforces.com/blog/entry/43256)
