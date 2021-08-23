# Tabela de Conteúdos
  * [O que é Programação Competitiva?](#o-que-é-programação-competitiva)
  * [Como funciona um problema de Programação Competitiva?](#como-funciona-um-problema-de-programação-competitiva)
  * [Solucionando o Problema de Programação Competitiva](#solucionando-o-problema-de-programação-competitiva)
  * [Submetendo a Solução](#submetendo-a-solução)
  * [O Juiz](#o-juiz)
  * [Vereditos](#vereditos)

## O que é Programação Competitiva?

Inicialmente, é necessário que não restem dúvidas para o leitor acerca das definições que estão sendo empregadas. Dessa forma, é possível descrever Programação Competitiva a partir da seguinte definição de um experiente programador competitivo [Ashar Fuadi](https://www.quora.com/What-is-competitive-programming-2/answer/Ashar-Fuadi)

> *“Competitive programming is solving well-defined problems by writing computer programs under specified limits”*

A definição acima pode ser livremente traduzida para o Português da seguinte maneira

> *“Programação Competitiva trata-se da resolução de problemas bem definidos mediante a escrita de programas de computador dentro de limites especificados"*

A partir da definição de Programação Competitiva, é possível ainda descrever com mais detalhes alguns termos presentes na definição, como *problemas bem definidos* e *programas de computador dentro de limites especificados*.

O termo *problemas bem definidos*, indica que cada problema de Programação Competitiva possuirá informações claras de como serão dispostas as informações de entrada e saída do programa, assim como considerações que o programador deve assumir sobre o enunciado, além de restrições sobre as variáveis envolvidas. Dessa maneira, um problema bem definido não abre margem para uma descrição ambígua sobre o que o programador deve efetuar para alcançar a solução do problema.

Quanto ao termo *programa de computador dentro de limites especificados*, este indica que o programa de computador desenvolvido para solucionar o problema não pode ser feito de qualquer forma, existem limites impostos pelo problema que devem ser respeitados, em geral os limites dizem respeito ao tempo de execução do código, o valor que os parâmetros do problema podem assumir e o tamanho de memória que o programa pode alocar no máximo, caso os limites do problema sejam ultrapassados ou não respeitados devidamente, então a solução não será considerada aceitável.

Após uma explicação mais detalhada da definição e de alguns trechos que fazem parte desta, pode ser que o leitor se veja confuso e na expectativa de exemplos de como essas definições se apresentam na prática. Dessa maneira, a próxima seção lidará diretamente com a explicação de um problema de Programação Competitiva.   

## Como funciona um problema de Programação Competitiva?

A imagem a seguir contém a descrição do problema [Média Inteira](https://neps.academy/br/exercise/136) retirado da Plataforma NEPS Academy.

<p align="center">
  <img src="/images/media-inteira-neps.png">
</p>

A partir da imagem, é possível separar o texto do problema em cinco principais seções: **Descrição do problema**, **Entrada e saída**, **Restrições** ,**Exemplos de teste** e **Limites**. É importante ressaltar que as cinco seções descritas sempre estarão presentes num problema de programação competitiva, pois são estas seções que garantem a definição de um *problema bem definido*.

A seguir têm-se uma definição mais elaborada de cada uma das cinco seções destacadas

* **Descrição do Problema**: Trata-se de uma seção inicial em que geralmente o escritor do problema define um contexto para então apresentar uma situação-problema que deve ser resolvida pelo programador. No entanto, em alguns casos (como no exemplo em questão) não existe uma contextualização da situação problema e a tarefa é proposta para o programador de maneira direta, sem que seja necessária uma interpretação do mesmo sob o texto. No exemplo em questão, o problema pede para o programador calcular a média inteira entre dois valores inteiros denotados por **A** e **B**. 

* **Entrada e Saída**: Após a descrição do problema e do que o programador deve solucionar, a seção de entrada e saída indica como devem ser inseridas e mostradas as informações que farão parte do problema. A **Entrada** diz respeito aos valores que serão inseridos no programa pelo teclado (ou por outros meios) para serem processados, e a **Saída** a como as respostas para o problema devem ser mostradas na tela. Como dito, a seção de entrada e saída indica EXATAMENTE como as informações correspondentes devem ser recebidas e mostradas pelo programa de computador, **caso as instruções dessa seção não sejam devidamente respeitadas, a solução não será considerada válida**.

* **Restrições**: A seção de restrições fornece uma descrição dos valores que os parâmetros do problema assumirão durante a correção da solução do programador. No exemplo em questão, a restrição indica que os valores inseridos na entrada e utilizados durante o processamento do programa não possuirão um valor absoluto maior que 1000, isto é, o programa com a solução será avaliado somente considerando casos em que os valores inseridos respeitam essa restrição. Dessa forma, se por acaso o programa não conseguir gerar médias inteiras com valores de entrada maiores que 1000, a resposta continuará sendo considerada como correta, pois a solução exige um cálculo de médias inteiras apenas pra números na entrada cujo valor absoluto seja menor ou igual a 1000.

* **Exemplos de Teste**: A seção fornece para o programador alguns exemplos de como o seu programa deve se comportar. Dessa maneira, são fornecidos alguns valores de entrada e saída, **respeitando as condições impostas na seção de Entrada e Saída**, e a lógica necessária para resolver o problema. Uma prática interessante é entender por que os casos de exemplo retornam determinada saída para uma dada entrada, pois assim o programador tem a confirmação de que este realmente entendeu o que o problema pede que seja solucionado. No exemplo em questão, o primeiro caso de teste conta com dois números inteiros de entrada (**2** e **2**) e um inteiro **2** na saída, isso indica que a operação de média inteira realizada entre os valores da entrada terá como resultado na saída o número **2**. Por fim, é importante ressaltar que os casos de teste pertencentes a seção não serão os únicos considerados durante a checagem da solução desenvolvida pelo programador, sendo assim, **resolver os casos de teste da seção de exemplos não é uma garantia de que sua solução está correta**.

* **Limites**: Os limites impostos pelo problema dizem respeito ao tempo máximo de execução que o programa deve levar para resolver um caso de teste e a quantidade de memória máxima que o programa irá alocar no computador para resolver cada caso de teste. De maneira resumida, um programa de computador pode demorar menos ou mais tempo para processar uma determinada quantidade de informações, assim como a quantidade de espaço alocada na memória pode variar, de acordo com a lógica do programa. No exemplo em tese, o tempo limite de execução do código é de 1 segundo e o espaço máximo que pode ser ocupado é de 256 megabytes (MB), **caso uma solução não respeite os limites de memória e tempo do problema, ela não será considerada aceitável**.

Finalmente, após identificar as principais seções que formam um problema de Programação Competitiva, podemos relacionar estas seções com a definição de programação competitiva vista no início deste artigo. Dessa maneira, pode-se dizer que as seções de **Descrição**, **Entrada e Saída** e **Exemplos de teste** tornam o problema proposto um *problema bem definido*. Ademais, a existência das **Restrições** e dos **Limites** necessitam que a solução do programador seja um *programa de computador dentro de limites especificados*. Sendo assim, o problema [Média Inteira](https://neps.academy/br/exercise/136) por se tratar de um problema bem-definido e necessitar de um programa de computador dentro de limites especificados para ser solucionado corretamente, **pode ser considerado um problema de Programação Competitiva**.

## Solucionando o Problema de Programação Competitiva

Após ter o entendimento de como se dá um tipico problema de Programação Competitiva, o próximo passo é entender como funciona o processo de solução de um problema do tipo.

Relendo a seção de **Descrição** do problema, identifica-se que é solicitado um programa de computador que gere, a partir de dois números inteiros na entrada, a média inteira desses dois valores. A média inteira entre dois valores pode ser entendido como a parte inteira da média entre números, sendo assim, para dois números **A** e **B**, a média inteira será sempre a parte inteira do resultado da operação **(A + B)/2**. Portanto, após identificar o que precisa ser feito para alcançar a solução, o próximo passo é a implementação.

Antes de seguirmos para a implementação, é necessário identificar que tipo de operações deverão ser realizadas para construir o programa de computador com a solução desejada. Sendo assim, podemos separar a nossa solução em três principais partes, que dizem respeito a como o programa deve funcionar

1. Receber os valores **A** e **B** do teclado (Entrada);
2. Realizar o cálculo da média inteira;
3. Mostrar o cálculo da média inteira (Saída);

Para solucionar o problema, utilizaremos a linguagem de programação C++ que é comumente utilizada em competições de programação.

**1. Receber os valores A e B do teclado (Entrada)**

A fim de solucionar essa parte do problema, é necessário identificar em nosso código que iremos utilizar funções que recebem informações do teclado e de outros lugares do computador para dentro do programa, então para poder utilizar essas funções incluimos a biblioteca [iostream](https://www.cplusplus.com/reference/iostream/) de C++ no topo do nosso código.

```cpp
#include <iostream> // Inclui no programa biblioteca que possui funções para entrada e saída
```

A seguir, criaremos a nossa função principal onde iremos condensar as principais instruções do nosso programa. A função é chamada de **main** por padrão e esta é declarada como um tipo inteiro. Além disso, de acordo com a seção **Entradas e Saídas** do problema, dois valores inteiros serão lidos na entrada do problema, a leitura de valores na entrada do programa pode ser realizada por meio da função **std::cin** de C++.

```cpp
#include <iostream>

int main(){
    int A, B; // Criação das variáveis inteiras que receberão dados da entrada.
    std::cin>>A>>B; // Lendo os valores registrados na entrada e guardando os mesmos em A e B, respectivamente.
    
}
```

O código acima já consegue criar duas variáveis inteiras **A** e **B** e então por meio da função **std::cin** é possível ler dois valores na entrada e guarda-los nas duas variáveis **A** e **B**, respectivamente.


**2. Realizar o cálculo da média inteira**

Agora que possuimos valores guardados em nossas variáveis **A** e **B**, podemos calcular a média inteira dos valores **A** e **B** ao considerar a parte inteira da operação **(A + B)/2**. Para considerarmos somente a parte inteira, basta que realizemos a operação salvando o resultado numa variável inteira, pois o C++ se encarregará de retirar a parte real do resultado antes de salva-lo na variável inteira (Para mais informações, leia sobre [divisão de inteiros](https://softwareengineering.stackexchange.com/questions/307993/why-does-integer-division-result-in-an-integer)). Sendo assim, criamos uma variável inteira **C** e guardamos o resultado da operação **(A + B)/2** nela.

```cpp
#include <iostream>

int main(){
    int A, B; // Criação das variáveis inteiras que receberão dados da entrada.
    std::cin>>A>>B; // Lendo os valores registrados na entrada e guardando os mesmos em A e B, respectivamente.
    int C = (A+B)/2; // Cria variável inteira C e guarda o resultado da média inteira nela;
}
```

**3. Mostrar o cálculo da média inteira (Saída);**

Finalmente, após ter em nosso programa uma maneira de salvar os valores **A** e **B** vindos da entrada e calcular a média inteira entre estes valores, basta mostrar o resultado da operação (que está guardado na variável **C**) na saída do programa. Para realizar a última etapa utilizamos a função **std::cout** e então exibimos a variável **C** em nossa saída. A seguir temos o código completo do programa 

```cpp
#include <iostream>

int main(){
    int A, B;
    std::cin>>A>>B;
    int C = (A+B)/2; 
    std::cout<<C;
}
```

## Submetendo a Solução

Após gerarmos um código para um programa de computador com a solução, podemos submeter a mesma solução utilizando o sistema de correções da plataforma em que o problema está inserido. Nesse problema, estamos usando a plataforma NEPS Academy, então basta clicar no botão **Escrever Solução**, selecionar a linguagem que está sendo utilizada para desenvolver a solução, colar o código da solução e então clicar no botão **Enviar**, conforme a imagem a seguir

<p align="center">
  <img src="/images/submissao-media-inteira.png">
</p>

Após clicar em **Enviar** o código será julgado e receberá um veredito. No caso do código desenvolvido neste guia, o veredito foi **Accepted**, isto é, significa que nosso programa de computador foi capaz de solucionar o problema proposto.

<p align="center">
  <img src="/images/media-inteira-accepted.png">
</p>

## O Juiz

Após entender as nuances de um problema de Programação Competitiva e até a solução de um, o leitor pode estar se perguntando sobre como os programas enviados para julgamento são corrigidos. O processo de correção de um exercício de programação competitiva conta com a existência de um programa de computador chamado **Juíz** (*Judge*), o Juíz é responsável por pegar as entradas de uma série de casos de testes relacionados ao problema que está sendo resolvido, inserir no programa de solução enviado pelo programador e então comparar as saídas geradas pelo programa de solução com as saídas corretas, além de verificar o tempo e a memória que sua aplicação está necessitando para resolver os casos de teste. Por conta disso que é tão importante que o programador siga de maneira rigorosa os critérios estabelecidos na seção de **Entrada e Saída** do problema, **pois caso a resposta esteja diferente daquela que o Juíz tem como resposta esperada, a solução não será aceita**.

## Vereditos

Retornando ao código da solução do problema Média Inteira, imagine que você cometeu um engano durante a operação de média inteira e esqueceu de dividir por dois durante o cálculo, resultando num código como o descrito abaixo

```cpp
#include <iostream>

int main(){
    int A, B;
    std::cin>>A>>B;
    int C = (A+B);  // Cálculo errôneo da média inteira 
    std::cout<<C;
}
```

Ao submeter a solução contendo esse engano no código, o Juíz irá gerar um veredito diferente do **Accepted**. Nesse caso, pelo fato da operação guardada na variável **C** não ser a operação de média inteira, então o veredito do Juíz é **Wrong Answer**, isto é, nosso programa não gera pelo menos uma das saídas como esperado.

<p align="center">
  <img src="/images/media-inteira-wa.png">
</p>

Além do **Accepted** e do **Wrong Answer**, existem outros tipos de vereditos que o Juíz pode retornar para o seu programa, alguns relacionados com a ultrapassagem dos limites de tempo ou de memória e outros relacionados com problemas de execução do seu código. Você pode realizar uma leitura sobre os tipos mais comuns de vereditos nesta página [Verdict information](https://onlinejudge.org/index.php?option=com_content&task=view&id=16&Itemid=31) do site [Online Judge](https://onlinejudge.org/index.php).

 
> Autor: Carlos Dias (CarZ)
