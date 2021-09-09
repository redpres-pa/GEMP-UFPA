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

Uma solução em C++ para o problema pode ser a seguinte:

```cpp
#include <iostream> 

using namespace std;

int main(){
  int n;
  int vetor[1000];
  int valor_maximo;

  cin>>n;
  
  for(int i = 0; i<n; i++){
    cin>>vetor[i];
  }

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

Ao comparar a quantidade de operações realizadas para os dois tipos de entradas diferentes, temos a resposta óbvia de que para um valor de entrada maior, o código em questão realiza uma quantidade maior de operações, e vice-versa.

Além disso, a quantidade de operações realizadas para este mesmo código será executado da mesma maneira em dois computadores com configurações de hardwares completamente diferentes, pois as linguagens de programação em geral funcionam de maneira independente das capacidades que o hardware pode oferecer. Portanto, a quantidade de operações realizadas para este código cresce da mesma maneira em um computador de última geração e em um computador da década passada.

Diante do exposto, concluimos que os parâmetros em um código, que por definição são independentes da quantidade de hardware alocado, afetam diretamente na eficiência que um algoritmo pode ter durante sua execução. De maneira geral, os parâmetros que influenciam diretamente nas operações são os **tamanhos da entrada do algoritmo descrito**. Logo, para um algoritmo que verifica o valor máximo em um array o parâmetro seria o tamanho do array inserido, já um algoritmo que compara as palavras em duas frases teria como parâmetro a quantidade de palavras por frase.

Ademais, um outro parâmetro diretamente relacionado com a eficiência de um algoritmo seria **a quantidade de operações elementares** que o algoritmo realiza. Por operações elementares entende-se as operações que são realizadas com frequência durante a execução de um código, e que por si só são rápidas de se realizar. No exemplo anterior, podemos tomar como operações básicas os seguintes trechos, denotados por **Op<sub>1</sub>**, **Op<sub>2</sub>**, **Op<sub>3</sub>** e **Op<sub>4</sub>**, respectivamente.


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

Então, podemos parametrizar a quantidade total operações básicas **Op<sub>Total</sub>** em função do tamanho do array **n**, pois sabemos que para um valor **n** da entrada as operações 2 e 3 ocorrem **n** vezes, tendo assim

<p style="text-align:center"> <b> Op<sub>Total</sub>(n) = Op<sub>1</sub> + n* Op<sub>2</sub> + n* Op<sub>3</sub> + Op<sub>4</sub> </b>

Então, podemos mensurar a complexidade temporal de um algoritmo por meio da quantidade de operações que a execução do algoritmo demanda para uma certa entrada. Além disso, de maneira similar podemos determinar a complexidade espacial de um algoritmo por meio da quantidade de espaço demandada para a execução do algoritmo. A seguir identificaremos maneiras de analisar essas complexidades por meio de um dispositivo mais formal e conhecido na matemática, os polinômios.

## Análise de Complexidade de Algoritmos

## Teorema da Aceleração Linear

## Notações Assintóticas

## Propriedades da Notação Big-O

## Exemplos

## Referências
 
> Autor: Carlos Dias (CarZ)
