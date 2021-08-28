# Conversão de DP Top-down para Bottom-up

Durante o treino no tópico de Programação Dinâmica, com o aumento do nível de dificuldade dos problemas vemos uma tendência de soluções com DP projetadas *Bottom up* ganhando mais relevância, seja por ser amigável a otimizações, ou por ter *constantes* menores. 
Porém, para maratonistas inexperientes projetar uma DP bottom up pode não ser uma tarefa fácil ~~e as vezes nada intuitivo~~, e tendem a se agarrar à implementação top-down, o que pode desacelerar seu ritmo de aprendizado.

> Para saber mais sobre as diferenças entre projetar DP de forma top-down ou bottom-up, acompanhe nosso projeto, em breve teremos um artigo tratando deste assunto!

Bom, embora pensar direto numa implementação bottom up possa ser um pouco dificíl de primeira, converter uma DP top down para bottom up é fácil.
Então temos a seguinte estratégia para implementar DP bottom up: Começar implementando top down, e depois converter de top down para bottom up.

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

Dessa forma vemos uma relação entre a resposta de quantas formas há de fazer soma *n* a partir de quantas formas há de fazer somas *n-1*, *n-2*, *n-3*, *n-4*, *n-5* e *n-6*. 
Mais especificamente, se criarmos uma função f(n) que significa "de quantas formas podemos obter soma n lançando dados de 6 faces", temos a seguinte relação *recursiva*:

```
f(n) = f(n-1) + f(n-2) + f(n-3) + f(n-4) + f(n-5) + f(n-6)
```

> Esse é um bom momento para observar que o problema que queremos resolver tem a propriedade de **subestrutura ótima**, dado que a resposta para o nosso problema depende da resposta de subproblemas mais simples.

Para completar nossa solução, precisamos agora definir os casos base dessa recursão. 
Casos base são aqueles subproblemas que são tão triviais que a resposta é quase óbvia, e você nem precisa pensar muito pra responder. 
No nosso problema são:

- Se n = 0, então f(n) = 1, pois só tem uma forma de fazer soma 0, que é **não fazer nada**. Se você quer fazer uma soma 0, então você não vai fazer nenhum lançamento, pois já tem a soma desejada, e essa **é uma forma válida de contar em combinatória**.

- Se n < 0, então f(n) = 0, pois não tem como você fazer uma soma negativa, dado que fazendo zero ou mais lançamentos a soma de faces obtida é sempre não negativa.

> Para saber mais sobre a opção de "não fazer nada" em combinatória leia este artigo (TODO: incluir link). 

Agora podemos implementar uma função que resolve nosso problema. 

```cpp
const int MOD = 1e9 + 7;
int f(int n) {
  if (n == 0) {
    return 1;
  }
  if (n < 0) {
    return 0;
  }

  int ans = 0;
  for (int i = 1; i <= 6; ++i) {
    ans += f(n-i);
    ans %= MOD;
  }
  return ans;
}
```

Porém, embora esta solução esteja correta, ela é muito **lenta**. De fato, a classe de complexidade temporal dessa solução é exponencial, em notação *Big-O* ela é `O(6^n)`. 
Mas, como sabemos, a lentidão dessa solução ocorre do fato de que um estado é recalculado várias e várias vezes, devido à **sobreposição de subproblemas**. Então, para melhorar nossa solução basta aplicar **memoization**:

```cpp
const int MOD = 1e9 + 7;
const int MAXN = 1e6 + 7;
int dp[MAXN];
bool seen[MAXN];

int f(int n) {
  if (n == 0) {
    return 1;
  }
  if (n < 0) {
    return 0;
  }

  //Se esse estado já foi calculado, retorne a resposta
  if (seen[n]) return dp[n];

  int ans = 0;
  for (int i = 1; i <= 6; ++i) {
    ans += f(n-i);
    ans %= MOD;
  }

  //marque o estado como calculado e guarde a resposta
  seen[n] = true;
  return dp[n] = ans;
}
```
E *voí la!* Com essas duas linhas de código agora a complexidade temporal do nosso algoritmo é `O(n)`, linear!! Sempre que calculamos alguma coisa guardamos essa informação em um tabela, e quando chegamos novamente em um estado previamente calculado, em vez de calcular tudo de novo só usamos a resposta guardada na tabela.

Agora que temos uma solução top-down para o nosso problema, podemos começar a conversão para bottom-up!

## Passo 1: Construir casos bases (TODO)




/* comentários Conversão DP top-down => DP bottom up


//1º passo - construir casos bases <=> base da recursão

//2º passo - definir ordem para calcular estados <=> ordem que vai percorrer a matriz

//(dica: se estiver difícil, desenha uma tabela, e faz setinha pra representar as dependências do que tem que estar calculado antes)

//3º passo - copia e cola as transições do top-down pro bottom-up

//4º passo - troca chamada recursiva pelo acesso do estado na tabela

//5º passo - guardar a resposta calculada

> Autor: Felipe Cardoso