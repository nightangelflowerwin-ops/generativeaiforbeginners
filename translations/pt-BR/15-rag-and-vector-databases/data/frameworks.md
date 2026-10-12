# Frameworks de Redes Neurais

Como já aprendemos, para treinar redes neurais de forma eficiente precisamos fazer duas coisas:

* Operar com tensores, por exemplo, multiplicar, somar e calcular algumas funções como sigmoid ou softmax
* Calcular gradientes de todas as expressões, para realizar a otimização por descida do gradiente

Embora a biblioteca `numpy` possa fazer a primeira parte, precisamos de algum mecanismo para calcular gradientes. No nosso framework que desenvolvemos na seção anterior, tivemos que programar manualmente todas as funções derivadas dentro do método `backward`, que realiza a retropropagação. Idealmente, um framework deveria nos permitir calcular gradientes de *qualquer expressão* que definirmos.

Outra coisa importante é poder realizar cálculos na GPU, ou em outras unidades especializadas de processamento, como TPU. O treinamento de redes neurais profundas exige *muitos* cálculos, e poder paralelizar esses cálculos em GPUs é fundamental.

> ✅ O termo 'paralelizar' significa distribuir os cálculos entre múltiplos dispositivos.

Atualmente, os dois frameworks de redes neurais mais populares são: TensorFlow e PyTorch. Ambos fornecem uma API de baixo nível para operar com tensores tanto na CPU quanto na GPU. Sobre essa API de baixo nível, existem também APIs de nível mais alto, chamadas Keras e PyTorch Lightning, respectivamente.

API de Baixo Nível | TensorFlow | PyTorch
------------------|------------|---------
API de Alto Nível | Keras      | PyTorch

As **APIs de baixo nível** em ambos os frameworks permitem construir os chamados **grafos computacionais**. Esse grafo define como calcular a saída (geralmente a função de perda) a partir dos parâmetros de entrada, e pode ser enviado para execução na GPU, se disponível. Existem funções para diferenciar esse grafo computacional e calcular gradientes, que podem ser usados para otimizar os parâmetros do modelo.

As **APIs de alto nível** consideram redes neurais basicamente como uma **sequência de camadas**, facilitando muito a construção da maioria das redes neurais. O treinamento do modelo geralmente requer preparar os dados e então chamar uma função `fit` para realizar o processo.

A API de alto nível permite construir redes neurais típicas muito rapidamente, sem se preocupar com muitos detalhes. Ao mesmo tempo, a API de baixo nível oferece muito mais controle sobre o processo de treinamento, sendo muito usada em pesquisas, quando se trabalha com arquiteturas novas de redes neurais.

Também é importante entender que você pode usar ambas as APIs juntas, por exemplo, pode desenvolver sua própria arquitetura de camada usando a API de baixo nível e depois usá-la dentro de uma rede maior construída e treinada com a API de alto nível. Ou pode definir uma rede usando a API de alto nível como uma sequência de camadas e depois usar seu próprio loop de treinamento de baixo nível para realizar a otimização. Ambas as APIs usam os mesmos conceitos básicos subjacentes e foram projetadas para funcionar bem juntas.

## Aprendizado

Neste curso, oferecemos a maior parte do conteúdo tanto para PyTorch quanto para TensorFlow. Você pode escolher seu framework preferido e seguir apenas os notebooks correspondentes. Se não souber qual escolher, leia algumas discussões na internet sobre **PyTorch vs. TensorFlow**. Também pode explorar ambos para entender melhor.

Sempre que possível, usaremos APIs de alto nível para simplificar. No entanto, acreditamos que é importante entender como redes neurais funcionam desde o básico, por isso começamos trabalhando com a API de baixo nível e tensores. Mas, se quiser começar rápido e não gastar muito tempo com esses detalhes, pode pular para os notebooks da API de alto nível.

## ✍️ Exercícios: Frameworks

Continue seu aprendizado nos seguintes notebooks:

API de Baixo Nível | Notebook TensorFlow+Keras | PyTorch
------------------|----------------------------|---------
API de Alto Nível | Keras                      | *PyTorch Lightning*

Depois de dominar os frameworks, vamos recapitular o conceito de overfitting.

# Overfitting

Overfitting é um conceito extremamente importante em aprendizado de máquina, e é fundamental entendê-lo bem!

Considere o problema de aproximar 5 pontos (representados por `x` nos gráficos abaixo):

!linear | overfit
-------------------------|--------------------------
**Modelo linear, 2 parâmetros** | **Modelo não linear, 7 parâmetros**
Erro de treinamento = 5.3 | Erro de treinamento = 0
Erro de validação = 5.1 | Erro de validação = 20

* À esquerda, vemos uma boa aproximação por uma linha reta. Como o número de parâmetros é adequado, o modelo captura corretamente a distribuição dos pontos.
* À direita, o modelo é muito poderoso. Como temos apenas 5 pontos e o modelo tem 7 parâmetros, ele pode se ajustar para passar por todos os pontos, fazendo o erro de treinamento ser zero. Porém, isso impede o modelo de entender o padrão correto dos dados, por isso o erro de validação é muito alto.

É muito importante encontrar um equilíbrio correto entre a complexidade do modelo (número de parâmetros) e a quantidade de amostras de treinamento.

## Por que o overfitting ocorre

  * Dados de treinamento insuficientes
  * Modelo muito complexo
  * Muito ruído nos dados de entrada

## Como detectar overfitting

Como você pode ver no gráfico acima, o overfitting pode ser detectado por um erro de treinamento muito baixo e um erro de validação alto. Normalmente, durante o treinamento, tanto o erro de treinamento quanto o de validação começam a diminuir, mas em algum momento o erro de validação pode parar de diminuir e começar a aumentar. Isso é um sinal de overfitting e indica que provavelmente devemos parar o treinamento nesse ponto (ou pelo menos salvar uma cópia do modelo).

overfitting

## Como prevenir overfitting

Se você perceber que está ocorrendo overfitting, pode fazer uma das seguintes coisas:

 * Aumentar a quantidade de dados de treinamento
 * Diminuir a complexidade do modelo
 * Usar alguma técnica de regularização, como Dropout, que veremos mais adiante.

## Overfitting e o Tradeoff Viés-Variância

Overfitting é, na verdade, um caso de um problema mais geral em estatística chamado Tradeoff Viés-Variância. Se considerarmos as possíveis fontes de erro no nosso modelo, podemos identificar dois tipos:

* **Erros de viés** são causados pelo algoritmo não conseguir capturar corretamente a relação entre os dados de treinamento. Isso pode acontecer porque o modelo não é poderoso o suficiente (**underfitting**).
* **Erros de variância** são causados pelo modelo aproximar o ruído dos dados de entrada em vez da relação significativa (**overfitting**).

Durante o treinamento, o erro de viés diminui (à medida que o modelo aprende a aproximar os dados) e o erro de variância aumenta. É importante parar o treinamento - seja manualmente (quando detectamos overfitting) ou automaticamente (introduzindo regularização) - para evitar o overfitting.

## Conclusão

Nesta aula, você aprendeu sobre as diferenças entre as várias APIs dos dois frameworks de IA mais populares, TensorFlow e PyTorch. Além disso, aprendeu sobre um tema muito importante: overfitting.

## 🚀 Desafio

Nos notebooks que acompanham esta aula, você encontrará 'tarefas' no final; trabalhe nos notebooks e complete as tarefas.

## Revisão & Estudo Autônomo

Pesquise sobre os seguintes tópicos:

- TensorFlow
- PyTorch
- Overfitting

Pergunte a si mesmo:

- Qual a diferença entre TensorFlow e PyTorch?
- Qual a diferença entre overfitting e underfitting?

## Exercício

Neste laboratório, você deverá resolver dois problemas de classificação usando redes totalmente conectadas de camada única e múltiplas camadas, utilizando PyTorch ou TensorFlow.

**Aviso Legal**:  
Este documento foi traduzido utilizando o serviço de tradução por IA [Co-op Translator](https://github.com/Azure/co-op-translator). Embora nos esforcemos para garantir a precisão, esteja ciente de que traduções automáticas podem conter erros ou imprecisões. O documento original em seu idioma nativo deve ser considerado a fonte autorizada. Para informações críticas, recomenda-se tradução profissional humana. Não nos responsabilizamos por quaisquer mal-entendidos ou interpretações incorretas decorrentes do uso desta tradução.