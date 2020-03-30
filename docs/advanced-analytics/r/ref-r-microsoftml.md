---
title: Biblioteca de funções do R do MicrosoftML
description: Introdução à biblioteca de funções do MicrosoftML no SQL Server 2016 R Services e nos Serviços de Machine Learning do SQL Server com R.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/06/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 450091bba39cf10e551b8da5e62993ca676c64af
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "73707920"
---
# <a name="microsoftml-r-library-in-sql-server"></a>MicrosoftML (biblioteca do R no SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

O **MicrosoftML** é uma biblioteca de funções do R da Microsoft que fornece algoritmos de aprendizado de máquina de alto desempenho. Ele inclui funções para treinamento e transformações, pontuação, análise de texto e imagem e extração de recursos para obtenção de valores dos dados existentes.

As APIs de Machine Learning foram desenvolvidas pela Microsoft para aplicativos internos de aprendizado de máquina e foram refinadas ao longo dos anos para dar suporte a alto desempenho em Big Data, usando processamento de vários núcleos e streaming de dados rápido. O MicrosoftML também inclui várias transformações para processamento de texto e imagem.

## <a name="full-reference-documentation"></a>Documentação de referência completa

A biblioteca do **MicrosoftML** é distribuída em vários produtos da Microsoft, mas o uso é o mesmo com a biblioteca no SQL Server ou em outro produto. Como as funções são as mesmas, a [documentação para funções individuais do RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) é publicada em apenas uma localização na [referência do R](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) para o Microsoft Machine Learning Server. Se existirem comportamentos específicos do produto, as discrepâncias serão indicadas na página de ajuda da função.

## <a name="versions-and-platforms"></a>Versões e plataformas

A biblioteca do **MicrosoftML** é baseada no R 3.4.3 e está disponível somente quando você instala um dos seguintes produtos ou downloads da Microsoft:

+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)
+ [Serviços de Machine Learning do SQL Server](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 ou posterior](https://docs.microsoft.com/machine-learning-server/)
+ [Microsoft R Client](set-up-a-data-science-client.md)

> [!NOTE]
> As versões completas do produto são somente Windows no SQL Server 2017. Há suporte no Windows e no Linux para o **MicrosoftML** no [SQL Server 2019](../../linux/sql-server-linux-setup-machine-learning.md).

## <a name="package-dependencies"></a>Dependências do pacote

Os algoritmos no **MicrosoftML** dependem do [RevoScaleR](ref-r-revoscaler.md) para:

+ Objetos de fonte de dados. Os dados consumidos pelas funções do **MicrosoftML** são criados usando funções do **RevoScaleR**.
+ Computação remota (mudança da execução da função para uma instância remota do SQL Server). A biblioteca do **RevoScaleR** fornece funções para criar e ativar um contexto de computação remota para o SQL Server.

Na maioria dos casos, você carregará os pacotes juntos sempre que estiver usando o **MicrosoftML**.

## <a name="functions-by-category"></a>Funções por categoria

Esta seção lista as funções por categoria para dar uma ideia de como cada uma é usada. Use também o [sumário](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) para localizar as funções em ordem alfabética.

<a name="ml-algorithms"></a>

## <a name="1-machine-learning-algorithms"></a>1 – Algoritmos de aprendizado de máquina

| Nome da função | Descrição |
|---------------|-------------|
|[rxFastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees) | Uma implementação de FastRank, uma implementação eficiente do algoritmo de gradient boosting MART.  |
|[rxFastForest](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastforest) | Uma implementação de floresta de regressão aleatória e de floresta quantil usando [rxFastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees).  |
|[rxLogisticRegression](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/logisticregression) | Regressão logística usando L-BFGS.  |
|[rxOneClassSvm](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxoneclasssvm) | Computador de vetor com suporte para uma classe.  
|[rxNeuralNet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet) | Rede neural de regressão binária e multiclasse.  |
|[rxFastLinear](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastlinear) | Otimização ascendente de coordenada dupla estocástica para classificação e regressão binárias lineares. |
|[rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble) | Treina diversos modelos de vários tipos para obter um melhor desempenho de previsão do que poderia ser obtido de um único modelo.|

<a name="ml-transforms"></a>

## <a name="2-transformation-functions"></a>2 – Funções de transformação

| Nome da função | Descrição |
|---------------|-------------|
|[concat](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/concat) | Transformação para criar uma coluna com valor de vetor única com base em várias colunas.  |
|[categorical](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categorical) | Criar vetor de indicador usando transformação categórica com dicionário.  |
|[categoricalHash](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categoricalhash) | Converte o valor categórico em uma matriz de indicadores por hash. |
|[featurizeText](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/featurizetext) | Produz uma bolsa de contagens de sequências de palavras consecutivas, chamadas n-grams, de um determinado corpus de texto. Oferece detecção de idioma, geração de tokens, remoção de palavras irrelevantes, normalização de texto e criação de recursos.  |
|[getSentiment](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/getsentiment) | Classifica o texto em idioma natural e cria uma coluna que contém probabilidades de que os sentimentos no texto sejam positivos.|
|[ngram](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/ngram) | permite definir argumentos para extração de recursos com base em contagem e em hash.|
|[selectColumns](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/selectcolumns) | Seleciona um conjunto de colunas para treinar novamente, descartando todas as outras. |
|[selectFeatures](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/selectfeatures) | Seleciona os recursos das variáveis especificadas usando um modo especificado.|
|[loadImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loadimage) | Carrega dados de imagem.|
|[resizeImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/resizeimage) | Redimensiona uma imagem para uma dimensão especificada usando um método de redimensionamento especificado.|
|[extractPixels](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/extractpixels) | Extrai os valores de pixel de uma imagem.|
|[featurizeImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/featurizeimage) | Aplica recursos a uma imagem usando um modelo de rede neural profunda pré-treinado.|


## <a name="3-scoring-and-training-functions"></a>3 – Funções de pontuação e de treinamento

| Nome da função | Descrição |
|---------------|-------------|
|[rxPredict.mlModel](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxpredict) | Executa a biblioteca de pontuação do SQL Server usando o procedimento armazenado ou do código R habilitando a pontuação em tempo real para fornecer um desempenho de previsão muito mais rápido.|
|[rxFeaturize](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfeaturize) | Transforma dados de um conjunto de dados de entrada em um conjunto de dados de saída.|
|[mlModel](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/mlmodel) | Fornece um resumo de um modelo de machine learning do Microsoft R.|


## <a name="4-loss-functions-for-classification-and-regression"></a>4 – Funções de perda para classificação e regressão

| Nome da função | Descrição |
|---------------|-------------|
|[expLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | Especificações para a função de perda de classificação exponencial. | 
|[logLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | Especificações para a função de perda de classificação de log.  |
|[hingeLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | Especificações para a função de perda de classificação de hinge. | 
|[smoothHingeLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | Especificações para a função de perda de classificação de smooth hinge.  |
| [poissonLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | Especificações da função de perda de regressão Poisson. | 
|[squaredLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | Especificações da função de perda de regressão quadrada.   |   

## <a name="5-feature-selection-functions"></a>5 – Funções de seleção de recurso

| Nome da função | Descrição |
|---------------|-------------|
|[minCount](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/mincount) | Especificação para seleção de recursos no modo de contagem. |
|[mutualInformation](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/mutualinformation) | Especificação para seleção de recursos no modo de informações mútuo. |

## <a name="6-ensemble-modeling-functions"></a>6 – Funções de modelagem do conjunto

| Nome da função | Descrição |
|---------------|-------------|
|[fastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/fasttrees) | Cria uma lista que contém o nome e os argumentos da função para treinar um modelo de Árvore Rápida com [rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble).|
|[fastForest](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastforest) | Cria uma lista que contém o nome e os argumentos da função para treinar um modelo de Floresta Rápida com [rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble).|
|[fastLinear](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/fastlinear) | Cria uma lista que contém o nome e os argumentos da função para treinar um modelo Linear Rápido com [rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble).|
|[logisticRegression](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/logisticregression) | Cria uma lista que contém o nome e os argumentos da função para treinar um modelo de Regressão Logística com [rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble).|
|[oneClassSvm](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/oneclasssvm) | Cria uma lista que contém o nome e os argumentos da função para treinar um modelo OneClassSvm com [rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble).|

## <a name="7-neural-networking-functions"></a>7 – Funções de rede neural

| Nome da função | Descrição |
|---------------|-------------|
|[optimizer](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/optimizer) | Especifica algoritmos de otimização para o algoritmo de aprendizado de máquina [rxNeuralNet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet).|


## <a name="8-package-state-functions"></a>8 – Funções de estado do pacote

| Nome da função | Descrição |
|---------------|-------------|
|[rxHashEnv](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxHashEnv) | Um objeto do ambiente usado para armazenar o estado de todo o pacote. |


## <a name="how-to-use-microsoftml"></a>Como usar o MicrosoftML

As funções do **MicrosoftML** podem ser chamadas no código R encapsulado em procedimentos armazenados. A maioria dos desenvolvedores cria soluções do **MicrosoftML** localmente e, em seguida, migra o código do R concluído para procedimentos armazenados como um exercício de implantação.

O pacote **MicrosoftML** para R é instalado "pronto para uso" no SQL Server 2017. Ele também está disponível para uso com o SQL Server 2016 se você atualiza os componentes do R para a instância: [Atualizar uma instância do SQL Server usando a associação](../install/upgrade-r-and-python.md)

O pacote não é carregado por padrão. Como uma primeira etapa, carregue o pacote **MicrosoftML** e carregue o **RevoScaleR** caso precise usar contextos de computação remota ou conectividade relacionada ou objetos de fonte de dados. Em seguida, faça referência às funções individuais de que você precisa.

```R
library(microsoftml);
library(RevoScaleR);
logisticRegression(args);
```

## <a name="see-also"></a>Confira também

+ [Tutoriais do R](../tutorials/sql-server-r-tutorials.md)
+ [Saiba como usar contextos de computação](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
+ [R para desenvolvedores do SQL: Treinar e colocar um modelo em operação](../tutorials/sqldev-in-database-r-for-sql-developers.md)
+ [Amostras de produtos da Microsoft no GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples)
+ [Referência do R (Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) 