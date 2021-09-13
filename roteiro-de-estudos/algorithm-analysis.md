# Tabela de Conteúdos
  * [Por que Analisar Algoritmos?](#o-que-é-programação-competitiva)
  * [Introdução a Análise de Algoritmos](#como-funciona-um-problema-de-programação-competitiva)
  * [Análise de Complexidade de Algoritmos](#solucionando-o-problema-de-programação-competitiva)
  * [Teorema da Aceleração Linear](#submetendo-a-solução)
  * [Notações Assintóticas](#o-juiz)
  * [Propriedades da Notação Big-O](#vereditos)
  * [Exemplos](#exemplos)
  * [Referências](#referencias)

## Por que Analisar Algoritmos?

Em programação e desenvolvimento de software, sabe-se que é possível desempenhar uma mesma tarefa ou construir uma mesma ideia utilizando diferentes abordagens em código. Nesse sentido, a existência de parâmetros que quantifiquem e promovam uma comparação de uma solução em relação a outra são fundamentais para entender a viabilidade destas em diferentes contextos. A fim de exemplificar, suponha que você possui um mesmo problema para resolver em duas situações diferentes: Você está desenvolvendo um software para funcionar em um sistema embarcado que possui alguns megabytes de memória disponíveis, você está desenvolvendo um mesmo software para uma aplicação alocada num servidor que atende milhões de usuários simultaneamente. Na primeira situação, espera-se que você utilize abordagens no seu código que consumam o mínimo possível de memória ao longo da execução do programa, uma vez que, resolver o problema consumindo mais memória do que o disponível torna sua solução irrealizável para esse contexto. Por outro lado, na segunda situação, o consumo de memória não é necessariamente um fator crítico para o funcionamento do programa, mas se o programa desenvolvido demandar tempo demais para atender todos os seus usuários, muitos poderão ficar insatisfeitos com a aplicação e vir a não utiliza-la novamente.

Além disso, em programação competitiva os problemas possuem limites de tempo de execução e memória disponível especificados, cujo o veredito da solução depende diretamente de respeitar os limites. Sendo assim, um programador competitivo também deve ter noção de como ponderar qualitativamente e quantitativamente as suas soluções no que diz respeito a tempo de execução e memória alocada, você pode pensar nos limites do problema como uma simulação de uma situação real, em que por algum motivo é exigido que a tarefa descrita no problema seja desempenhada dentro do tempo e consumindo no máximo a memória especificada. 

Portanto, analisar parâmetros como quantidade de memória alocada e tempo de execução de um algoritmo são fatores que podem ser determinantes para um programador julgar qual abordagem este pode utilizar dentro do contexto do seu problema, e foi mediante a existência dessa necessidade que surgiu o estudo da Análise de Algoritmos. Ao longo deste artigo serão discutidos os aspectos fundamentais da análise de algoritmos para identificar maneiras de classificar com propriedade soluções diferentes para um mesmo problema no que diz respeito a tempo de execução e memória alocada. 

## Introdução a Análise de Algoritmos

A análise de algoritmos pode ser entendida como o processo de definição dos parâmetros que se fazem necessários para a execução de um algoritmo num computador, a fim de determinar quantitativamente a sua eficiência quanto a diversos fatores, sendo os principais o **tempo de execução (ou complexidade temporal)** e a **quantidade de memória alocada (ou complexidade espacial)**.

Após ter conhecimento da definição do termo, uma dúvida comum que surge seria a de se realmente faz sentido um estudo voltado para análise de eficiência de um algoritmo, haja vista que em termos práticos a velocidade de execução de um código depende diretamente do hardware utilizado para executá-lo. Sendo assim, é comum pensar que um mesmo algoritmo executado num computador de última geração terá uma execução mais veloz do que se feito num computador da década passada,o que é verdade. No entanto, existem métricas num código que independem do tipo de hardware envolvido, como por exemplo a quantidade de operações realizadas durante a execução, o tamanho dos valores da entrada e os tipos de dados envolvidos. Nesse sentido, a análise de algoritmos se vale destes tipos de informações contidas num código para quantificar a eficiência espacial e temporal do mesmo, **tornando-a um dispositivo independente do tipo de hardware utilizado**.

A seguir, é possível propor o seguinte problema para elucidar os tipos de parâmetros que serão avaliados na análise de algoritmos.

> Para um array de tamanho **n**, identifique o maior elemento contido dentro do array.

Um algoritmo que resolve o problema em C++ pode ser o seguinte:

```cpp
#include <iostream> 

using namespace std;

int main(){
  int n;

  cin>>n;

  int vetor[n];

  for(int i = 0; i<n; i++){
    cin>>vetor[i];
  }

  int valor_maximo;

  for(int i = 0; i<n; i++){
    if(i == 0){
      valor_maximo = vetor[i]; 
    }
    else{
      valor_maximo = max(valor_maximo, vetor[i]);
    }
  }

  cout<<valor_maximo<<'\n';
  return 0;  
}
```

Sabe-se que um programa pode ser visto como um fluxo de operações que ocorre um numero predeterminado de vezes e segue uma ordem estabelecida. Dessa forma, ao executar o código acima para um valor de **n = 1**, podemos reescrever a execução dos laços em função da  quantidade operações realizadas da seguinte maneira

```cpp
{  
  cin>>n;

  i = 0;
  cin>>vetor[i];
  
  i = 0;
  if(i == 0){
    valor_maximo = vetor[i]; 
  }
  else{
    valor_maximo = max(valor_maximo, vetor[i]);
  }

  cout<<valor_maximo<<'\n';
  return 0;  
}
```

De maneira análoga, podemos reescrever o programa da seguinte forma para uma entrada com **n = 3**.

```cpp
{
  cin>>n;
    
  i = 0;
  cin>>vetor[i];
  i = 1;
  cin>>vetor[i];
  i = 2;
  cin>>vetor[i];
  

  i = 0;
  if(i == 0){
    valor_maximo = vetor[i]; 
  }
  else{
    valor_maximo = max(valor_maximo, vetor[i]);
  }
  i = 1;
  if(i == 0){
    valor_maximo = vetor[i]; 
  }
  else{
    valor_maximo = max(valor_maximo, vetor[i]);
  }
  i = 2;
  if(i == 0){
    valor_maximo = vetor[i]; 
  }
  else{
    valor_maximo = max(valor_maximo, vetor[i]);
  }

  cout<<valor_maximo<<'\n';
  return 0;  
}
```

Ao comparar a quantidade de operações realizadas para os dois tipos de entradas diferentes, temos a conclusão óbvia de que para um valor de entrada maior, o código em questão realiza uma quantidade maior de operações.

Além disso, a quantidade de operações realizadas para este mesmo código será executado da mesma maneira em dois computadores com configurações de hardwares completamente diferentes, pois as linguagens de programação em geral funcionam de maneira independente das capacidades que o hardware pode oferecer. Portanto, a quantidade de operações realizadas para este código cresce de maneira idêntica em um computador de última geração e em um computador da década passada.

Concluimos portanto que os parâmetros em um código, que por definição são independentes da quantidade de hardware alocado, afetam diretamente na eficiência que um algoritmo pode ter durante sua execução. De maneira geral, os parâmetros que influenciam diretamente nas operações são os **tamanhos da entrada do algoritmo descrito**. Logo, para um algoritmo que verifica o valor máximo em um array o parâmetro seria o tamanho do array inserido, já um algoritmo que compara as palavras em duas frases teria como parâmetro a quantidade de palavras por frase, por exemplo.

Ademais, um outro parâmetro diretamente relacionado com a eficiência de um algoritmo seria **a quantidade de operações elementares** que o algoritmo realiza. Operações elementares são aquelas realizadas com frequência durante a execução de um código, e que por si só são rápidas de se realizar. No exemplo anterior, podemos tomar como operações básicas os seguintes trechos.


```cpp
{
  /* Operação Básica 1 */
  cin>>n;

  /* Operação Básica 2 */  
  cin>>vetor[i];
  
  /* Operação Básica 3 */
  if(i == 0){
    valor_maximo = vetor[i]; 
  }
  else{
    valor_maximo = max(valor_maximo, vetor[i]);
  }

  /* Operação Básica 4 */
  cout<<valor_maximo<<'\n';
  return 0;  
}
```

Então, podemos parametrizar a quantidade total operações básicas **Op<sub>Total</sub>** em função do tamanho do array **n**, pois sabemos que para um valor **n** da entrada as operações 2 e 3 ocorrem **n** vezes. Por outro lado, as operações 1 e 4 ocorrem somente uma vez independentemente do tamanho da entrada, tendo assim

<p style="text-align:center"> <b> Op<sub>Total</sub>(n) = 1 + n + n + 1 </b>

Então, podemos mensurar a **complexidade temporal de um algoritmo por meio da quantidade de operações que a execução do algoritmo demanda em função de um certo parâmetro, geralmente relacionado com a entrada**. Além disso, de maneira análoga podemos determinar a **complexidade espacial de um algoritmo por meio da quantidade de espaço demandada para a execução do algoritmo**. A seguir iremos explorar de maneira mais aprofundada como extrair de outros códigos esse tipo de estrutura matemática representada por **Op<sub>Total</sub>**, que para este caso nada mais é do que um polinômio.

## Análise de Complexidade de Algoritmos

Retomando a equação que descreve a quantidade de operações que serão realizadas pelo algoritmo proposto acima

<p style="text-align:center"> <b> Op<sub>Total</sub>(n) = 1 + n + n + 1 </b>

Ao analisar a equação acima, percebe-se que é possível estimar o tempo total de execução do programa se caso fosse conhecido o tempo demandado para cada uma das quatro operações destacadas na equação. No entanto, determinar de maneira precisa o tempo demandado para cada uma dessas operações pode variar conforme o tipo de linguagem de programação, compilador e arquitetura do hardware utilizado, tornando uma análise por esse viés algo dificil de se generalizar. Apesar dessa dificuldade de estimar, sabemos que operações como **comparação de dados, atribuição de tipos de dados básicos da linguagem e leituras de entrada e saída** são vistas como básicas, e portanto de rápida execução, na maioria das linguagens de programação. Dessa forma, afim de simplificar nossa análise é possível assumir que as operações  possuem mesma ordem de grandeza e portanto possuem influência semelhante na estimativa de eficiência temporal do algoritmo, o que nos permite reescrever a relação acima como 

<p style="text-align:center"> <b> Op<sub>Total</sub>(n) = 2 + 2*n  </b>

O que de fato representa quantitativamente a quantidade de operações básicas que será executada, dado a entrada. Caso **n = 0**, então **Op<sub>Total</sub>(0) = 2**, isto é, o algoritmo não será executado pois não há máximos num array vazio, restando apenas a execução das operações de entrada e saída. Caso **n = 3**, então **Op<sub>Total</sub>(3) = 2 + 6 = 8**, que é a mesma quantidade de operações básicas destacadas na representação da execução demonstrada acima.

Dessa forma, ao estudar o comportamento de um algoritmo podemos estimar fatores como eficiência temporal ao modelar a quantidade de operações em funções de parâmetros relevantes à execução do algoritmo (geralmente o tamanho da entrada).

A seguir estudaremos mais três algoritmos e extrairemos a quantidade de operações que serão realizadas com elas em relação a um parâmetro.

## Problema 1

> Para um array de tamanho **n**, identifique se existem elementos idênticos dentro do array.

Para esse problema, uma solução direta (mas não tão eficiente) para esse problema seria a seguinte:

```cpp
#include<iostream>

using namespace std;

int main(){
  int n;

  cin>>n;

  int vetor[10000];

  for(int i = 0; i< n; i++){
    cin>>vetor[i];
  }

  bool existe_repeticao = false;

  for(int i = 0; i<n; i++){
    for(int j= 0; j<n; j++){
      if(i != j && vetor[i] == vetor[j]){
        existe_repeticao = true;
        break;
      }
    }
  }

  if(existe_repeticao){
    cout<<"Há repetições\n";
  }
  else{
    cout<<"Não há repetições\n";
  }

  return 0;
}
```

A ideia por trás desta solução está em comparar todos os elementos do array um com o outro e identificar se há a existência de elementos com o mesmo valor, caso exista o laço de verificação é interrompido e a execução do código é alterada para indicar a existência de repetições, caso não existam elementos idênticos após todas as verificações, o código informa que não há elementos idênticos no array.

Analisando o código, é possível identificar que a etapa de verificação do array é composta de dois laços, em que o primeiro laço (indexado em **i**) percorre o array do primeiro até o último valor, e para cada uma das execuções do primeiro laço, este executa o segundo laço (indexado em **j**) que também acessa todos os valores contidos no array e realiza a operação de comparação do valor indexado em **i** com o valor indexado em **j**. Dessa forma, podemos tomar a operação de comparação do valor indexado em **i** com o valor indexado em **j** como sendo a **operação básica de funcionamento do algoritmo**, pois independente do tamanho de **n**, o funcionamento do algoritmo se dá pela existência da comparação destes valores. Sendo assim, é possível destacar as operações básicas do código acima da seguinte maneira


```cpp
#include<iostream>

using namespace std;

int main(){
  /* Operação 1 */
  cin>>n;

  /* Operação 2 */
  cin>>vetor[i];
  
  /* Operação 3 */
  {
  .
  .
  .
  if(i != j && vetor[i] == vetor[j]){
    existe_repeticao = true;
    break;
  }
  .
  .
  .
  }
  /* Operação 4 */
  if(existe_repeticao){
    cout<<"Há repetições\n";
  }
  else{
    cout<<"Não há repetições\n";
  }
}
```

A partir do trecho descrito acima, percebe-se que as operações 1 e 4 ocorrem apenas uma vez, independente do valor da entrada **n**. Além disso, a operação 2 é similar a operação 2 observada no algoritmo para achar o valor máximo num array, sendo executada **n** vezes. Por fim, a contagem de vezes que a operação 3 é executada pode ser calculada da seguinte forma: A operação 3 é executada **n** vezes por conta do segundo laço, que por sua vez, é executado **n** vezes por conta do primeiro laço, conforme a seguinte relação:  

<div style="text-align:center">
  <img src="https://render.githubusercontent.com/render/math?math=\sum_{i%20=%200}^{n-1}\sum_{j=%200}^{n-1} \cdot 1%20%20=%20n\cdot%20n%20=%20n^2">
</div>

Logo, é possível determinar a relação **Op<sub>Total</sub>(n)** somando a quantidade de vezes que cada operação será realizada em função de **n**.

<div style="text-align:center">
  <img src="https://render.githubusercontent.com/render/math?math=\textrm{Op}_{\textrm{total}}(n)%20%20%20=%201%20%2B%201%20%2B%20n%20%2B%20n^2%20=%202%20%2B%20n%20%2B%20n^2">
</div>

Ao definir **Op<sub>Total</sub>(n)** para este problema é possível ter uma noção interessante da velocidade de execução deste algoritmo em relação ao algoritmo que busca o máximo valor em um array. O algoritmo atual é um algoritmo cujo o número de operações é modelado por um polinômio do segundo grau, enquanto que o algoritmo do valor máximo é descrito como um polinômio do primeiro grau. Sendo assim, para um mesmo valor de **n**, temos que o algoritmo atual tende a realizar mais operações que o algoritmo do valor máximo. Além disso, uma outra noção interessante identificada em ambos os problemas é que a existência de uma estrutura de repetição (como loops) torna a quantidade de operações básicas realizadas existentes dentro da estrutura em loop função do número de repetições.

# Problema 2

> Dado um valor inteiro. Retorne o equivalente em binário dele.

Nesse problema, o objetivo é implementar o algoritmo de conversão de números de base decimal para base binária. O algoritmo funciona da seguinte forma: a partir do número inicial, dividimos o número por dois e salvamos o resultado desta operação e seu resto, e então dividimos o resultado desta operação por dois novamente salvando o resto e o resultado, até que o resultado das sucessivas operações de divisão deixe de ser divisível por dois. Por fim, a representação em binária do número será a concatenação de todos os valores de resto encontrados, você pode ler mais sobre o algoritmo de conversão binário para decimal no site [Calcular e Converter](https://calculareconverter.com.br/converter-decimal-para-binario/). A figura abaixo foi retirada do site [Calcular e Converter](https://calculareconverter.com.br/converter-decimal-para-binario/) e mostra o esquema de conversão do número 25 da base decimal para a base binária aplicando o algoritmo sugerido

<p style="text-align:center">
  <img src="/images/decimal-em-binario.png">
</p>

Dessa maneira, é possível implementar esse algoritmo em C++ da seguinte forma

```cpp
#include <iostream>
#include <string>
using namespace std;

int main(){
  int n;

  cin>>n;

  int resposta[100];
  int i = 0;

  while(n >= 2){
    int resto = n%2;
    int resultado = n/2;

    resposta[i] = resto;
    n = resultado;
    i++;
  }

  resposta[i] = n;

  for(int j = i; j>=0; j--){
      cout<<resposta[j];
  }
  cout<<'\n';
  return 0;
}
```

Novamente, a fim de calcular a quantidade de operações realizadas pelo algoritmo, podemos representar a execução do algoritmo como a concatenação de operações básicas, que nesse caso se dão da seguinte maneira.

```cpp
#include <iostream>
#include <string>
using namespace std;

int main(){
  /* Operação Básica 1 */
  cin>>n;

 /* Operação Básica 2*/
  int resto = n%2;
  int resultado = n/2;

  resposta[i] = resto;
  n = resultado;
  i++;
  

  /* Operação Básica 3 */
  resposta[i] = n;

  /* Operação Básica 4 */
  cout<<resposta[j];
  
  cout<<'\n';
  return 0;
}
```

Ao análisar o código percebemos que as operações básicas 1 e 3 ocorrem somente uma vez para qualquer valor de n. No entanto, o laço de repetição que gera os parâmetros para as operações básicas 2 e 4 não é igual ao valor do tamanho da entrada, uma vez que a repetição da operação 2 ocorre enquanto a entrada for divisível por dois. Além disso, o loop da operação 4 tem o mesmo tamanho da quantidade de repetições do loop da operação 2. Nesse sentido, é necessário que identifiquemos uma relação do valor da entrada **n** com a quantidade de repetições geradas pelos loops a fim de representar uma função **Op<sub>Total</sub>(n)** que relacione as operações realizadas pelo algoritmo em função da entrada.

Ao observar o fluxo de execução do algoritmo, percebe-se que o valor inicial **n** acaba sendo dividido por 2 **i** vezes, que também é a quantidade de vezes que o loop da operação básica 2 é executado. Sendo assim, tomando um **n** qualquer, é possível representar a cada repetição o seu novo valor da seguinte forma

<div style="text-align:center">
  <img src="https://render.githubusercontent.com/render/math?math=%5B%20n%20%2C%20\dfrac{n}{2}%20%2C%20\dfrac{n}{4}%20%2C%20\dfrac{n}{8}%20%2C%20...%20%5D">
</div>

Observando o comportamento do valor de **n** ao longo das repetições do loop em questão, identifica-se que o decrescimento de **n** pode ser visto como uma **Progressão Geométrica de razão 1/2**. Dessa forma, podemos utilizar a fórmula para encontrar o termo final de uma Progressão Geométrica, que encerra o laço de repetição, dado pelo valor 1 (pois se **n** inicia maior ou igual a 2, o menor resultado que pode ser definido da divisão de **n** por 2 é igual a 1). Além de saber o valor final da progressão analisada, sabemos que esta progressão ocorrerá após **i** repetições, sendo assim, calcula-se o valor do termo **a<sub>i-1</sub>(n)**

<div style="text-align:center">
  <img src="https://render.githubusercontent.com/render/math?math=a_{k}%20=%20a_{1}%20\cdot%20q^{k-1};%20">
</div>

<div style="text-align:center">
  <img src="https://render.githubusercontent.com/render/math?math=a_{1}%20=%20n%20%3B%20%20q%20=%20\dfrac{1}{2}%20%3B%20k%20=%20i%20%3B">
</div>

<div style="text-align:center">
  <img src="https://render.githubusercontent.com/render/math?math=1%20=%20n%20\cdot%20(\dfrac{1}{2})^{i-1}">
</div>

<div style="text-align:center">
  <img src="https://render.githubusercontent.com/render/math?math=2^{i-1}%20=%20n">
</div>

Aplicando logaritmo na base 2 em ambos os lados da equação, temos o número de repetições **i** em função do tamanho do valor **n**

<div style="text-align:center">
  <img src="https://render.githubusercontent.com/render/math?math=\log_{2}{(n)}%20=%20i%20-%201">
</div>

<div style="text-align:center">
  <img src="https://render.githubusercontent.com/render/math?math=\log_{2}{(n)} + 1 = i ">
</div>

Por fim, dado que as operações 2 e 4 estão dentro de um loop que se repete **i** vezes, e sendo **i** representado através do valor da entrada, é possível escrever a função **Op<sub>Total</sub>(n)** para o algoritmo abaixo como sendo

<div style="text-align:center">
  <img src="https://render.githubusercontent.com/render/math?math=\textrm{Op}_{\textrm{total}}(n)%20=%202%20%2B%20\log{2}{(n)}%20%2B%201%20%2B%20\log{2}{(n)}%20%2B%201%20=%20%20%204%20%2B%202%20\cdot%20\log{2}{(n)}">
</div>

Após solucionar o problema 2, percebe-se que nem sempre o número de execuções de uma operação é igual ao tamanho do parâmetro de entrada do algoritmo, dependendo da maneira como as condições do código são impostas, a quantidade de operações executadas pode ser escrita em função da variável de entrada de outras maneiras. Além disso, ao comparar a função **Op<sub>Total</sub>(n)** do problema atual com as funções calculadas anteriormente, percebemos que este algoritmo executa menos operações que todos os outros algoritmos mostrados acima para valores elevados de **n**, para **n = 32 o algoritmo do problema atual executa 14 operações ao total, enquanto que o algoritmo do problema 1 executa 1192 operações, por exemplo**.

A seguir, analisaremos um último algoritmo a fim de identificar um comportamento interessante neste.

# Problema 3

> Dado um valor de **n**, calcule o **n-ésimo** número da sequência de Fibonacci.



## Teorema da Aceleração Linear

## Notações Assintóticas

## Propriedades da Notação Big-O

## Exemplos

## Referências
 
> Autor: Carlos Dias (CarZ)
