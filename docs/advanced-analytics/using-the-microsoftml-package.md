---
title: Usando o pacote MicrosoftML com o SQL Server | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 51ffa33bef7ab880704c9c1391a69feb3e194202
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38984558"
---
# <a name="using-the-microsoftml-package-with-sql-server"></a>Usando o pacote MicrosoftML com o SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

O [ **MicrosoftML** ](https://msdn.microsoft.com/microsoft-r/microsoftml-introduction) pacote que é fornecido com o Microsoft R Server e SQL Server 2017 inclui vários algoritmos de aprendizado de máquina. Essas APIs foram desenvolvidos pela Microsoft para aplicativos de aprendizado de máquina interna e foram refinadas ao longo dos anos para dar suporte a alto desempenho em big data, usando o processamento de vários núcleos e streaming rápido de dados. MicrosoftML também inclui várias transformações para processamento de imagens e texto.

No SQL Server 2017 CTP 2.0, foi adicionado suporte para a linguagem Python. O **microsoftml** de pacote para Python contém funções equivalentes aos em que o pacote MicrosoftML para R. 

+ **MicrosoftML para R**

    Referência de pacote e de Introdução: [MicrosoftML: algoritmos de R de aprendizado de máquina](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)

    Porque o R diferencia maiusculas de minúsculas, certifique-se de que você referencie o nome corretamente ao carregar o pacote.

+ **microsoftml para Python**

    Referência de Introdução e pacote: [microsoftml (biblioteca de funções para o Python)](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package). 

## <a name="whats-in-microsoftml"></a>O que está em MicrosoftML

MicrosoftML contém uma variedade de transformações que foram otimizadas para desempenho e algoritmos de aprendizado de máquina.

### <a name="machine-learning-algorithms"></a>Algoritmos de aprendizado de máquina

-  Modelos lineares: `rxFastLinear` é um aprendiz linear com base na coordenada dupla alheatória que pode ser usada para classificação binária ou regressão. O modelo dá suporte a regularização L1 e L2.

- Modelos de florestas de decisão e de árvore de decisão: `rxFastTree` é um algoritmo de árvore de decisão aumentada, originalmente conhecido como FastRank, que foi desenvolvido para uso no Bing. É um dos aprendizes mais rápidos e mais populares. Dá suporte a regressão e classificação binária.

  `rxFastForest` um modelo de regressão logística com base no método de floresta aleatória. É semelhante à função `rxLogit` do RevoScaleR, mas dá suporte à regularização L1 e L2. Dá suporte a regressão e classificação binária.

- Regressão logística: `rxLogisticRegression` é um modelo de regressão logística semelhante ao `rxLogit` função do RevoScaleR, com suporte adicional para regularização L1 e L2. Dá suporte à classificação multiclasse ou binária.

- Redes neurais: O `rxNeuralNet` função dá suporte a classificação binária, classificação multiclasse e regressão usando redes neurais. Redes complicadas personalizáveis e dá suporte a aceleração de GPU, usando uma única GPU.

- Detecção de anomalias.  O `rxOneClassSvm` função se baseia no método SVM, mas é otimizada para classificação binária em conjuntos de dados desbalanceados.

### <a name="transformation-functions"></a>Funções de transformação

MicrosoftML inclui várias funções especializadas que são úteis para transformar os dados e extrair recursos.

- Recursos de processamento de texto incluem o `featurizeText` e `getSentiment` funções. Contagem de n-gramas, detectar o idioma usado ou executar a normalização do texto. Você também pode executar a limpeza de operações, como remoção de palavras irrelevantes de texto comum ou gerar recursos de baseada em contagem ou hash do texto.

- Seleção de recursos e funções de transformação de recursos, como `selectFeatures` ou `getSentiment`, analisar os dados e criar recursos que são mais úteis para modelagem.

- Trabalhar com variáveis categóricas usando, como `categorical` ou `categoricalHash`, qual converter valores categóricos em matrizes indexadas para melhorar o desempenho.

- Funções específicas ao processamento de imagens e análise, tais como `extractPixels` ou `featurizeImage`, permitem que você obtenha mais informações sobre imagens e processar imagens com mais rapidez.

Para obter mais informações, consulte [Funções do MicrosoftML](https://msdn.microsoft.com/microsoft-r/microsoftml/microsoftml).

## <a name="how-to-use-microsoftml"></a>Como usar o MicrosoftML

Esta seção descreve como localizar e carregar o pacote no seu código R e Python.

+ O pacote MicrosoftML para R é instalado por padrão com o Microsoft R Server 9.1.0 e no SQL Server 2017.

    Ele também está disponível para uso com o SQL Server 2016, se você atualizar os componentes do R para a instância usando o instalador do Microsoft R Server conforme descrito aqui: [atualizar uma instância do SQL Server usando a associação](r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)

+ O **microsoftml** do pacote do Python é instalado por padrão com o SQL Server 2017 

   Para usar este pacote, é recomendável que você atualize para a versão Release Candidate 2 ou posterior. Uma versão anterior foi lançada com o RC1, mas a biblioteca passou por revisão considerável, inclusive alterações em nomes de função. 

No entanto, para R e Python, o pacote não é carregado por padrão. Assim, você deverá carregar o pacote explicitamente como parte do seu código para usar suas funções.

### <a name="calling-microsoftml-functions-from-r-in-sql-server"></a>Chamando funções do MicrosoftML de R no SQL Server

Em seu código R, carregar o pacote MicrosoftML e chamar suas funções, como qualquer outro pacote.

```R
library(microsoftml);
library(RevoScaleR);
logisticRegression(args);
```

**Observações**

+ O pacote MicrosoftML é totalmente integrado com o pipeline de processamento de dados fornecido pelo pacote RevoScaleR. Assim, você pode usar o pacote MicrosoftML em qualquer contexto de computação baseados em Windows, incluindo uma instância do SQL Server que tem extensões de aprendizado de máquina habilitadas.

    No entanto, MicrosoftML requer uma referência ao RevoScaleR e suas funções para usar remoto contextos de computação.

### <a name="calling-microsoftml-functions-from-python-in-sql-server"></a>Chamando funções do microsoftml do Python no SQL Server

Para chamar funções do pacote, no código do Python, importe as **microsoftml** do pacote e, em seguida, importe **revoscalepy** se você precisar usar contextos de computação remota ou a fonte de dados ou conectividade relacionados objetos. Em seguida, fazer referência a funções individuais que você precisa.

```Python
from microsoftml.modules.logistic_regression.rx_logistic_regression import rx_logistic_regression
from revoscalepy.functions.RxSummary import rx_summary
from revoscalepy.etl.RxImport import rx_import_datasource
```

**Observações**

+ No SQL Server 2017, **microsoftml** é um módulo Python35 compatível. 

+ As funções na **microsoftml** são integrados com as fontes de dados e contextos de computação que são suportadas pelo **revoscalepy**. Assim, você pode usar o **microsoftml** pacote do Python para criar e pontuação de modelos em qualquer contexto de computação baseados em Windows, incluindo uma instância do SQL Server que tem extensões de aprendizado de máquina. habilitada.

    No entanto, **microsoftml** para Python requer uma referência a **revoscalepy** e contextos de computação de suas funções para usar o remoto.

Para obter mais informações sobre revoscalepy, consulte:

+ [O que é revoscalepy](python/what-is-revoscalepy.md)

+ [biblioteca de funções revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package) 
