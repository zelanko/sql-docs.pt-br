---
title: Biblioteca de funções do MicrosoftML R - serviços do SQL Server Machine Learning
description: Introdução à biblioteca de funções MicrosoftML no SQL Server 2016 R Services e os serviços do SQL Server 2017 Machine Learning com R.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/04/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 37f52a5ac891ab1d52a9b6335a62fdf2789df9b1
ms.sourcegitcommit: ee76332b6119ef89549ee9d641d002b9cabf20d2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/20/2018
ms.locfileid: "53645305"
---
# <a name="microsoftml-r-library-in-sql-server"></a>MicrosoftML (biblioteca de R no SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

**MicrosoftML** é uma biblioteca de funções de R da Microsoft, fornecendo os algoritmos de aprendizado de máquina de alto desempenho. Ele inclui funções para treinamento e transformações, pontuação, análise de texto e imagem e extração de recursos para derivar valores de dados existentes.

A aprendizado de máquina APIs foram desenvolvidas pela Microsoft para aplicativos de aprendizado de máquina interna e foram refinadas ao longo dos anos para dar suporte a alto desempenho em big data, usando o processamento de vários núcleos e streaming rápido de dados. MicrosoftML também inclui várias transformações para processamento de imagens e texto.

## <a name="full-reference-documentation"></a>Documentação de referência completo

O **MicrosoftML** biblioteca é distribuída em vários produtos da Microsoft, mas o uso é o mesmo se você obter a biblioteca no SQL Server ou outro produto. Porque as funções são os mesmos, [documentação para funções de RevoScaleR individuais](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) for publicado em apenas um local sob a [referência de R](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) para Microsoft Machine Learning Server. Deve qualquer produto específico comportamentos existirem, serão observadas o discrepâncias na página de ajuda de função.

## <a name="versions-and-platforms"></a>As versões e plataformas

O **MicrosoftML** biblioteca é com base em R 3.4.3 e está disponível apenas quando você instala um dos seguintes produtos da Microsoft ou downloads:

+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)
+ [Serviços de aprendizado de máquina do SQL Server 2017](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 ou posterior](https://docs.microsoft.com/machine-learning-server/)
+ [Microsoft R client](set-up-a-data-science-client.md)

> [!NOTE]
> São versões de lançamento de produto completo somente Windows, começando com o SQL Server 2017. Suporte do Linux para **MicrosoftML** há de novo no [visualização do SQL Server de 2019](../../linux/sql-server-linux-setup-machine-learning.md).

## <a name="package-dependencies"></a>Dependências do pacote

Algoritmos **MicrosoftML** dependem [RevoScaleR](ref-r-revoscaler.md) para:

+ Objetos de fonte de dados. Dados consumidos por **MicrosoftML** funções são criadas usando **RevoScaleR** funções.
+ Computação (execução de mudança de função para uma instância remota do SQL Server) remoto. O **RevoScaleR** biblioteca fornece funções para criação e ativação remota de computação do contexto para o SQL server.

Na maioria dos casos, você carregará os pacotes juntos sempre que você estiver usando **MicrosoftML**.

## <a name="functions-by-category"></a>Funções por categoria

Esta seção lista as funções por categoria para lhe dar uma ideia de como cada um deles é usado. Você também pode usar o [sumário](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) para localizar funções em ordem alfabética.

<a name="ml-algorithms"></a>

## <a name="1-machine-learning-algorithms"></a>Algoritmos de aprendizado de máquina 1

| Nome da função | Descrição |
|---------------|-------------|
|[rxFastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees) | Uma implementação de FastRank, uma implementação eficiente do gradiente MART algoritmo impulsionado.  |
|[rxFastForest](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastforest) | Uma floresta aleatória e a implementação de floresta de regressão de quantil usando [rxFastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees).  |
|[rxLogisticRegression](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/logisticregression) | Regressão logística usando L-BFGS.  |
|[rxOneClassSvm](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxoneclasssvm) | Máquinas de vetor de suporte de uma classe.  
|[rxNeuralNet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet) | Binária, multiclasse e regressão rede neural.  |
|[rxFastLinear](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastlinear) | Otimização de coordenada dupla alheatória para regressão e classificação binária linear. |
|[rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble) | Treina um número de modelos de vários tipos para obter melhor desempenho de previsão que pode ser obtido de um único modelo.|

<a name="ml-transforms"></a>

## <a name="2-transformation-functions"></a>Funções de transformação 2

| Nome da função | Descrição |
|---------------|-------------|
|[concat](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/concat) | Transformação para criar uma única coluna com valor de vetor de várias colunas.  |
|[categorical](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categorical) | Crie um vetor de indicador usando a transformação categórica com dicionário.  |
|[categoricalHash](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categoricalhash) | Converte o valor categórico em uma matriz de indicador pelo hash. |
|[featurizeText](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/featurizetext) | Produz um conjunto de contagens de sequências de palavras consecutivas, chamadas de n-gramas, de um determinado corpo de texto. Ele oferece detecção de idioma, geração de tokens, a remoção de palavras irrelevantes, normalização do texto e geração de recursos.  |
|[getSentiment](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/getsentiment) | Pontuações de texto de linguagem natural e cria uma coluna que contém as probabilidades que as opiniões no texto são positivas.|
|[ngram](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/ngram) | permite definir argumentos para extração de recursos baseados em hash e contagem.|
|[selectColumns](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/selectcolumns) | Seleciona um conjunto de colunas para treinar novamente, removendo todos os outros. |
|[selectFeatures](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/selectfeatures) | Seleciona os recursos usando as variáveis especificadas usando o modo especificado.|
|[loadImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loadimage) | Carrega dados de imagem.|
|[resizeImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/resizeimage) | Redimensiona uma imagem para uma dimensão especificada usando um método de redimensionamento especificado.|
|[extractPixels](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/extractpixels) | Extrai os valores de pixel de uma imagem.|
|[featurizeImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/featurizeimage) | Featurizes uma imagem usando um modelo de rede neural profunda pré-treinada.|


## <a name="3-scoring-and-training-functions"></a>Funções de treinamento e pontuação de 3

| Nome da função | Descrição |
|---------------|-------------|
|[rxpredict. Mlmodel](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxpredict) | Executa a biblioteca de pontuação do SQL Server, usando o procedimento armazenado, ou de código de R, permitindo a pontuação em tempo real fornecer muito mais rápido desempenho de previsão.|
|[rxFeaturize](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfeaturize) | Transforma os dados de um conjunto de dados de entrada para um conjunto de dados de saída.|
|[mlModel](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/mlmodel) | Fornece um resumo de um modelo de aprendizado de máquina do Microsoft R.|


## <a name="4-loss-functions-for-classification-and-regression"></a>Funções de perda de 4 para classificação e regressão

| Nome da função | Descrição |
|---------------|-------------|
|[expLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | Especificações de função de perda de classificação exponencial. | 
|[logLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | Especificações de função de perda de classificação de log.  |
|[hingeLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | Especificações de função de perda de classificação de integridade. | 
|[smoothHingeLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | Especificações de função de perda de classificação de integridade suave.  |
| [poissonLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | Especificações de função de perda de regressão de poisson. | 
|[squaredLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | Especificações de função de perda de quadrados de regressão.   |   

## <a name="5-feature-selection-functions"></a>Funções de seleção de recursos 5

| Nome da função | Descrição |
|---------------|-------------|
|[minCount](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/mincount) | Especificação de seleção de recursos no modo de contagem. |
|[mutualInformation](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/mutualinformation) | Especificação de seleção de recursos no modo de informações mútuas. |

## <a name="6-ensemble-modeling-functions"></a>Funções de modelagem de ensemble 6

| Nome da função | Descrição |
|---------------|-------------|
|[fastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/fasttrees) | Cria uma lista que contém o nome da função e os argumentos para treinar um modelo de árvore do Fast com [rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble).|
|[fastForest](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastforest) | Cria uma lista que contém o nome da função e os argumentos para treinar um modelo de floresta do Fast com [rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble).|
|[fastLinear](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/fastlinear) | Cria uma lista que contém o nome da função e os argumentos para treinar um modelo Linear rápidos com [rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble).|
|[logisticRegression](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/logisticregression) | Cria uma lista que contém o nome da função e os argumentos para treinar um modelo de regressão logística com [rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble).|
|[oneClassSvm](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/oneclasssvm) | Cria uma lista que contém o nome da função e os argumentos para treinar o modelo com OneClassSvm [rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble).|

## <a name="7-neural-networking-functions"></a>Funções de rede neural de 7

| Nome da função | Descrição |
|---------------|-------------|
|[Otimizador](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/optimizer) | Especifica os algoritmos de otimização para o [rxNeuralNet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet) algoritmo de aprendizado de máquina.|


## <a name="8-package-state-functions"></a>Funções de estado do pacote de 8

| Nome da função | Descrição |
|---------------|-------------|
|[rxHashEnv](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxHashEnv) | Um objeto de ambiente usado para armazenar o estado de todo o pacote. |


## <a name="how-to-use-microsoftml"></a>Como usar o MicrosoftML

Funções em **MicrosoftML** podem ser chamados no código R encapsulado em procedimentos armazenados. A maioria dos desenvolvedores construir **MicrosoftML** localmente, soluções e, em seguida, migrar código de R concluído para procedimentos armazenados como um exercício de implantação.

O **MicrosoftML** de pacote para o R é instalado "out-of-the-box" no SQL Server 2017. Ele também está disponível para uso com o SQL Server 2016 se você atualizar os componentes do R para a instância: [Atualizar uma instância do SQL Server usando a associação](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)

Não é possível carregar o pacote por padrão. Como uma primeira etapa, carregue o **MicrosoftML** do pacote e, em seguida, carregue **RevoScaleR** se você precisa usar contextos de computação remota ou objetos de fonte de dados ou conectividade relacionados. Em seguida, fazer referência a funções individuais que você precisa.

```R
library(microsoftml);
library(RevoScaleR);
logisticRegression(args);
```

## <a name="see-also"></a>Confira também

+ [Tutoriais de R](../tutorials/sql-server-r-tutorials.md)
+ [Saiba como usar contextos de computação](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
+ [R para desenvolvedores do SQL: Treinar e operacionalizar um modelo](../tutorials/sqldev-in-database-r-for-sql-developers.md)
+ [Exemplos de produtos da Microsoft no GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples)
+ [Referência de R (Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) 