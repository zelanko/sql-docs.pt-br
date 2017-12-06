---
title: Usando o pacote de MicrosoftML com o SQL Server | Microsoft Docs
ms.custom: 
ms.date: 08/23/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: R
ms.assetid: 1c377717-e281-431e-8171-3924dcce1cdd
caps.latest.revision: "132"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 02c2e0da0f6f0ee1b90fc9cbaf84569d9d8f08a1
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/01/2017
---
# <a name="using-the-microsoftml-package-with-sql-server"></a>Usando o pacote de MicrosoftML com o SQL Server

O [ **MicrosoftML** ](https://msdn.microsoft.com/microsoft-r/microsoftml-introduction) pacote que é fornecido com o Microsoft R Server e SQL Server 2017 inclui vários algoritmos de aprendizado de máquina. Essas APIs foram desenvolvidas pela Microsoft para aplicativos de aprendizado de máquina interna e foram refinadas ao longo dos anos para dar suporte a alto desempenho em grandes de dados, usando o fluxo de dados rápidos e processamento de vários núcleos. MicrosoftML também inclui várias transformações para processamento de imagem e texto.

No SQL Server de 2017 CTP 2.0, foi adicionado suporte para a linguagem Python. O **microsoftml** pacote para Python contém funções equivalentes no pacote MicrosoftML r. 

+ **MicrosoftML para R**

    Referência de pacote e introdução: [MicrosoftML: algoritmos de R de aprendizado de máquina](https://docs.microsoft.com/en-us/r-server/r-reference/microsoftml/microsoftml-package)

    Como R diferencia maiusculas de minúsculas, certifique-se de que você referenciar o nome corretamente ao carregar o pacote.

+ **microsoftml para Python**

    Referência de pacote e introdução: [microsoftml (biblioteca de funções para Python)](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package). 

## <a name="whats-in-microsoftml"></a>Novidades no MicrosoftML

MicrosoftML contém uma variedade de transformações que foi otimizadas para desempenho e algoritmos de aprendizado de máquina.

### <a name="machine-learning-algorithms"></a>Algoritmos de aprendizado de máquina

-  Modelos lineares: `rxFastLinear` um aprendiz linear se baseia estocástico ascendente coordenada duplo que pode ser usado para classificação binária ou regressão. O modelo dá suporte a regularização L1 e L2.

- Modelos de floresta de decisão e de árvore de decisão: `rxFastTree` é um algoritmo de árvore de decisão impulsionada originalmente conhecido como FastRank, que foi desenvolvido para uso no Bing. É um dos aprendizes mais rápidos e mais populares. Dá suporte a regressão e classificação binária.

  `rxFastForest`um modelo de regressão logística com base no método aleatória de floresta. É semelhante à função `rxLogit` do RevoScaleR, mas dá suporte à regularização L1 e L2. Dá suporte a regressão e classificação binária.

- Regressão logística: `rxLogisticRegression` é um modelo de regressão logística semelhante para o `rxLogit` função em RevoScaleR, com suporte adicional para regularização L1 e L2. Oferece suporte à classificação binária ou multiclasse.

- Redes neurais: O `rxNeuralNet` function dá suporte à classificação binária, classificação multiclasse e regressão usando redes neurais. Personalizável e oferece suporte a redes diferentes com a aceleração de GPU, usando uma GPU único.

- Detecção de anomalias.  O `rxOneClassSvm` função é baseada no método SVM, mas é otimizada para classificação binária desbalanceadas em conjuntos de dados.

### <a name="transformation-functions"></a>Funções de transformação

MicrosoftML inclui várias funções especializadas que são úteis para transformar dados e extrair recursos.

- Recursos de processamento de texto incluem o `featurizeText` e `getSentiment` funções. Contagem de n-grams, detectar o idioma usado ou executar a normalização do texto. Você também pode executar a limpeza de operações, como a remoção de palavras irrelevantes de texto comuns ou gerar recursos com base em contagem ou hash do texto.

- Seleção de recursos e funções de transformação de recursos, como `selectFeatures` ou `getSentiment`, analisar dados e criar recursos que são mais úteis para modelagem.

- Trabalhar com variáveis categóricas usando como `categorical` ou `categoricalHash`, qual converter valores categóricos em matrizes indexadas para melhorar o desempenho.

- Funções específicas para análise e processamento de imagem, como `extractPixels` ou `featurizeImage`, permitem que você obter mais informações sobre imagens e processar as imagens mais rápido.

Para obter mais informações, consulte [Funções do MicrosoftML](https://msdn.microsoft.com/microsoft-r/microsoftml/microsoftml).

## <a name="how-to-use-microsoftml"></a>Como usar MicrosoftML

Esta seção descreve como localizar e carregar o pacote no seu código R e Python.

+ O pacote de MicrosoftML para R está instalado por padrão com o Microsoft R Server 9.1.0 e no SQL Server 2017.

    Ele também está disponível para uso com o SQL Server 2016, se você atualizar os componentes de R para a instância usando o instalador do Microsoft R Server conforme descrito aqui: [atualizar uma instância do SQL Server usando a associação](r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)

+ O **microsoftml** para Python é instalado por padrão com o SQL Server 2017 do pacote 

   Para usar este pacote, é recomendável que você atualize para o Release Candidate 2 ou posterior. Uma versão anterior foi lançada com o RC1, mas a biblioteca passou por revisão considerável, inclusive alterações em nomes de função. 

No entanto, para R e Python, o pacote não é carregado por padrão. Assim, você deverá carregar o pacote explicitamente como parte do seu código para usar suas funções.

### <a name="calling-microsoftml-functions-from-r-in-sql-server"></a>Chamando funções de MicrosoftML de R no SQL Server

Em seu código R, carregar o pacote de MicrosoftML e chame as funções, como qualquer outro pacote.

```R
library(microsoftml);
library(RevoScaleR);
logisticRegression(args);
```

**Observações**

+ O pacote de MicrosoftML está totalmente integrado com o pipeline de processamento de dados fornecido pelo pacote RevoScaleR. Assim, você pode usar o pacote de MicrosoftML em qualquer contexto de computação baseados em Windows, incluindo uma instância do SQL Server que tem extensões de aprendizado de máquina habilitadas.

    No entanto, MicrosoftML requer uma referência a RevoScaleR e suas funções para usar remoto contextos de computação.

### <a name="calling-microsoftml-functions-from-python-in-sql-server"></a>Chamando funções de microsoftml do Python no SQL Server

Para chamar as funções do pacote, no seu código Python, importar o **microsoftml** do pacote e, em seguida, importe **revoscalepy** se você precisar usar contextos de computação remota ou a fonte de dados ou conectividade relacionados objetos. Em seguida, fazer referência as funções individuais, que você precisa.

```Python
from microsoftml.modules.logistic_regression.rx_logistic_regression import rx_logistic_regression
from revoscalepy.functions.RxSummary import rx_summary
from revoscalepy.etl.RxImport import rx_import_datasource
```

**Observações**

+ No SQL Server de 2017, **microsoftml** é um módulo Python35 compatível. 

+ As funções em **microsoftml** são integradas com as fontes de dados e contextos de computação que são suportadas pelo **revoscalepy**. Assim, você pode usar o **microsoftml** pacote do Python para criar e pontuação de modelos em qualquer contexto de computação baseados em Windows, incluindo uma instância do SQL Server que tem extensões de aprendizado de máquina. habilitado.

    No entanto, **microsoftml** para Python requer uma referência a **revoscalepy** e suas funções para usar remoto contextos de computação.

Para obter mais informações sobre revoscalepy, consulte:

+ [O que é revoscalepy](python/what-is-revoscalepy.md)

+ [biblioteca de funções revoscalepy](https://docs.microsoft.com/en-us/r-server/python-reference/revoscalepy/revoscalepy-package) 
