---
title: Biblioteca de funções do MicrosoftML R
description: Introdução à biblioteca de funções MicrosoftML no SQL Server 2016 R Services e SQL Server 2017 Serviços de Machine Learning com R.
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 2cf89b26ffad2902223a84e19ccaf425aa6f8b2d
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344904"
---
# <a name="microsoftml-r-library-in-sql-server"></a>MicrosoftML (R library in SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

**MicrosoftML** é uma biblioteca de funções do R da Microsoft que fornece algoritmos de aprendizado de máquina de alto desempenho. Ele inclui funções para treinamento e transformações, pontuação, análise de texto e imagem e extração de recursos para derivar valores de dados existentes.

As APIs de Machine Learning foram desenvolvidas pela Microsoft para aplicativos de aprendizado de máquina internos e foram refinadas ao longo dos anos para dar suporte a alto desempenho em Big Data, usando processamento de vários núcleos e streaming de dados rápido. O MicrosoftML também inclui várias transformações para o processamento de texto e imagem.

## <a name="full-reference-documentation"></a>Documentação de referência completa

A biblioteca **MicrosoftML** é distribuída em vários produtos da Microsoft, mas o uso é o mesmo se você obter a biblioteca em SQL Server ou em outro produto. Como as funções são as mesmas, a [documentação para funções individuais RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) é publicada em apenas um local sob a [referência de R](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) para Microsoft Machine Learning Server. Se existirem comportamentos específicos do produto, as discrepâncias serão indicadas na página de ajuda da função.

## <a name="versions-and-platforms"></a>Versões e plataformas

A biblioteca **MicrosoftML** é baseada em R 3.4.3 e disponível somente quando você instala um dos seguintes produtos ou downloads da Microsoft:

+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)
+ [SQL Server 2017 Serviços de Machine Learning](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 ou posterior](https://docs.microsoft.com/machine-learning-server/)
+ [Cliente do Microsoft R](set-up-a-data-science-client.md)

> [!NOTE]
> As versões completas de lançamento do produto são somente Windows, a partir do SQL Server 2017. O suporte do Linux para **MicrosoftML** é novo na versão [prévia do SQL Server 2019](../../linux/sql-server-linux-setup-machine-learning.md).

## <a name="package-dependencies"></a>Dependências do pacote

Os algoritmos no **MicrosoftML** dependem do [RevoScaleR](ref-r-revoscaler.md) para:

+ Objetos de fonte de dados. Os dados consumidos pelas funções **MicrosoftML** são criados usando as funções **RevoScaleR** .
+ Computação remota (mudança da execução da função para uma instância de SQL Server remota). A biblioteca **RevoScaleR** fornece funções para criar e ativar um contexto de computação remota para o SQL Server.

Na maioria dos casos, você carregará os pacotes ao mesmo tempo em que estiver usando o **MicrosoftML**.

## <a name="functions-by-category"></a>Funções por categoria

Esta seção lista as funções por categoria para dar uma ideia de como cada uma é usada. Você também pode [usar o Sumário](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) para localizar funções em ordem alfabética.

<a name="ml-algorithms"></a>

## <a name="1-machine-learning-algorithms"></a>1-algoritmos de aprendizado de máquina

| Nome da função | Descrição |
|---------------|-------------|
|[rxFastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees) | Uma implementação de FastRank, uma implementação eficiente do algoritmo de aumento de gradiente MART.  |
|[rxFastForest](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastforest) | Uma floresta aleatória e uma implementação de floresta de regressão Quantil usando [rxFastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfasttrees).  |
|[rxLogisticRegression](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/logisticregression) | Regressão logística usando L-BFGS.  |
|[rxOneClassSvm](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxoneclasssvm) | Uma classe dá suporte a máquinas de vetor.  
|[rxNeuralNet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet) | Rede neural binária, multiclasse e regressão.  |
|[rxFastLinear](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastlinear) | Otimização ascendente de coordenada dupla estocástico para classificação e regressão binária linear. |
|[rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble) | Treina diversos modelos de vários tipos para obter um melhor desempenho de previsão do que pode ser obtido a partir de um único modelo.|

<a name="ml-transforms"></a>

## <a name="2-transformation-functions"></a>2-funções de transformação

| Nome da função | Descrição |
|---------------|-------------|
|[concat](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/concat) | Transformação para criar uma única coluna de valor de vetor de várias colunas.  |
|[categorical](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categorical) | Criar vetor de indicador usando transformação categórica com dicionário.  |
|[categoricalHash](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/categoricalhash) | Converte o valor categórico em uma matriz de indicador por hash. |
|[featurizeText](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/featurizetext) | Produz uma bolsa de contagens de seqüências de palavras consecutivas, chamadas n-grams, de um determinado corpus de texto. Ele oferece detecção de idioma, geração de tokens, remoção de palavras irrelevantes, normalização de texto e criação de recursos.  |
|[getSentiment](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/getsentiment) | Classifica o texto em idioma natural e cria uma coluna que contém probabilidades de que as opiniões no texto são positivas.|
|[ngram](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/ngram) | permite definir argumentos para extração de recursos baseados em contagem e em hash.|
|[selectColumns](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/selectcolumns) | Seleciona um conjunto de colunas para treinar novamente, descartando todas as outras. |
|[selectFeatures](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/selectfeatures) | Seleciona os recursos das variáveis especificadas usando um modo especificado.|
|[loadImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loadimage) | Carrega dados de imagem.|
|[resizeImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/resizeimage) | Redimensiona uma imagem para uma dimensão especificada usando um método de redimensionamento especificado.|
|[extractPixels](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/extractpixels) | Extrai os valores de pixel de uma imagem.|
|[featurizeImage](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/featurizeimage) | Featurizes uma imagem usando um modelo de rede neural de nível pretreinado.|


## <a name="3-scoring-and-training-functions"></a>3-funções de classificação e de treinamento

| Nome da função | Descrição |
|---------------|-------------|
|[rxPredict.mlModel](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxpredict) | Executa a biblioteca de Pontuação de SQL Server, usando o procedimento armazenado ou do código R, habilitando a pontuação em tempo real para fornecer um desempenho de previsão muito mais rápido.|
|[rxFeaturize](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfeaturize) | Transforma dados de um conjunto de dados de entrada em um conjunto de dados de saída.|
|[mlModel](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/mlmodel) | Fornece um resumo de um modelo de Machine Learning do Microsoft R.|


## <a name="4-loss-functions-for-classification-and-regression"></a>4-funções de perda para classificação e regressão

| Nome da função | Descrição |
|---------------|-------------|
|[expLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | Especificações para a função de perda de classificação exponencial. | 
|[logLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | Especificações para a função de perda de classificação de log.  |
|[hingeLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | Especificações para a função de perda de classificação da dobradiça. | 
|[smoothHingeLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | Especificações para função de perda de classificação de dobradiça suave.  |
| [poissonLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | Especificações da função de perda de regressão Poisson. | 
|[squaredLoss](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/loss) | Especificações para a função de perda de regressão em quadrado.   |   

## <a name="5-feature-selection-functions"></a>5-funções de seleção de recursos

| Nome da função | Descrição |
|---------------|-------------|
|[minCount](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/mincount) | Especificação para seleção de recursos no modo de contagem. |
|[mutualInformation](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/mutualinformation) | Especificação para seleção de recursos no modo de informações mútuo. |

## <a name="6-ensemble-modeling-functions"></a>6-Ensemble funções de modelagem

| Nome da função | Descrição |
|---------------|-------------|
|[fastTrees](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/fasttrees) | Cria uma lista que contém o nome e os argumentos da função para treinar um modelo de árvore rápida com [rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble).|
|[fastForest](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxfastforest) | Cria uma lista que contém o nome da função e argumentos para treinar um modelo de floresta rápida com [rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble).|
|[fastLinear](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/fastlinear) | Cria uma lista que contém o nome e os argumentos da função para treinar um modelo rápido linear com [rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble).|
|[logisticRegression](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/logisticregression) | Cria uma lista que contém o nome e os argumentos da função para treinar um modelo de regressão logística com [rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble).|
|[oneClassSvm](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/oneclasssvm) | Cria uma lista que contém o nome e os argumentos da função para treinar um modelo OneClassSvm com [rxEnsemble](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxensemble).|

## <a name="7-neural-networking-functions"></a>7-funções de rede neural

| Nome da função | Descrição |
|---------------|-------------|
|[otimizador](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/optimizer) | Especifica algoritmos de otimização para o algoritmo de aprendizado de máquina [rxNeuralNet](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxneuralnet) .|


## <a name="8-package-state-functions"></a>8-funções de estado do pacote

| Nome da função | Descrição |
|---------------|-------------|
|[rxHashEnv](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxHashEnv) | Um objeto de ambiente usado para armazenar o estado de todo o pacote. |


## <a name="how-to-use-microsoftml"></a>Como usar o MicrosoftML

As funções no **MicrosoftML** são chamáveis em código R encapsulado em procedimentos armazenados. A maioria dos desenvolvedores cria soluções **MicrosoftML** localmente e, em seguida, migra o código R concluído para procedimentos armazenados como um exercício de implantação.

O pacote **MicrosoftML** para R é instalado "pronto para uso" no SQL Server 2017. Ele também estará disponível para uso com o SQL Server 2016 se você atualizar os componentes do R para a instância do: [Atualizar uma instância do SQL Server usando a associação](../install/upgrade-r-and-python.md)

O pacote não é carregado por padrão. Como uma primeira etapa, carregue o pacote **MicrosoftML** e, em seguida, carregue **RevoScaleR** se precisar usar contextos de computação remota ou objetos de fonte de dados ou conectividade relacionada. Em seguida, referencie as funções individuais de que você precisa.

```R
library(microsoftml);
library(RevoScaleR);
logisticRegression(args);
```

## <a name="see-also"></a>Confira também

+ [Tutoriais de R](../tutorials/sql-server-r-tutorials.md)
+ [Aprenda a usar contextos de computação](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
+ [R para desenvolvedores do SQL: Treinar e colocar um modelo em operação](../tutorials/sqldev-in-database-r-for-sql-developers.md)
+ [Exemplos de produtos da Microsoft no GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples)
+ [Referência de R (Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/r-reference/introducing-r-server-r-package-reference) 