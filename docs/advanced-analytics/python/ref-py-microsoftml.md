---
title: microsoftml pacote do Python - serviços do SQL Server Machine Learning
description: Apresenta a algoritmos de aprendizado de máquina da Microsoft e modelos para o Python, em relação às cargas de trabalho de aprendizado de máquina do SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/04/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 618c4b127c42aae6a5b8d7570f1962f8c8e38e9a
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58511713"
---
# <a name="microsoftml-python-module-in-sql-server"></a>microsoftml (módulo de Python no SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

**microsoftml** é um módulo Python35 compatível da Microsoft, fornecendo os algoritmos de aprendizado de máquina de alto desempenho. Ele inclui funções para treinamento e transformações, pontuação, análise de texto e imagem e extração de recursos para derivar valores de dados existentes.

A aprendizado de máquina APIs foram desenvolvidas pela Microsoft para aplicativos de aprendizado de máquina interna e foram refinadas ao longo dos anos para dar suporte a alto desempenho em big data, usando o processamento de vários núcleos e streaming rápido de dados. Esse pacote foi originado como equivalente de uma versão de R, Python [MicrosoftML](../r/ref-r-microsoftml.md), que tem funções semelhantes. 

## <a name="full-reference-documentation"></a>Documentação de referência completo

O **microsoftml** biblioteca é distribuída em vários produtos da Microsoft, mas o uso é o mesmo se você obter a biblioteca no SQL Server ou outro produto. Porque as funções são iguais, [documentação para funções do microsoftml individuais](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) é publicado para apenas um local sob a [referência de Python](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference) para Microsoft Machine Learning Server. Deve qualquer produto específico comportamentos existirem, serão observadas o discrepâncias na página de ajuda de função.

## <a name="versions-and-platforms"></a>As versões e plataformas

O **microsoftml** módulo é com base em Python 3.5 e está disponível apenas quando você instala um dos seguintes produtos da Microsoft ou downloads:

+ [SQL Server 2017 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 ou posterior](https://docs.microsoft.com/machine-learning-server/)
+ [Bibliotecas de cliente do Python para um cliente de ciência de dados](setup-python-client-tools-sql.md)

> [!NOTE]
> São versões de lançamento de produto completo somente Windows, começando com o SQL Server 2017. Suporte do Linux para **microsoftml** há de novo no [visualização do SQL Server de 2019](../../linux/sql-server-linux-setup-machine-learning.md).

## <a name="package-dependencies"></a>Dependências do pacote

Algoritmos **microsoftml** dependem [revoscalepy](ref-py-revoscalepy.md) para:

+ Objetos de fonte de dados. Dados consumidos por **microsoftml** funções são criadas usando **revoscalepy** funções.
+ Computação (execução de mudança de função para uma instância remota do SQL Server) remoto. O **revoscalepy** biblioteca fornece funções para criação e ativação remota de computação do contexto para o SQL server.

Na maioria dos casos, você carregará os pacotes juntos sempre que você estiver usando **microsoftml**.

## <a name="functions-by-category"></a>Funções por categoria

Esta seção lista as funções por categoria para lhe dar uma ideia de como cada um deles é usado. Você também pode usar o [sumário](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference) para localizar funções em ordem alfabética.

## <a name="1-training-functions"></a>Funções de treinamento de 1

| Função | Descrição |
|----------|-------------|
|[microsoftml.rx_ensemble](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-ensemble) | Treine um ensemble de modelos. |
|[microsoftml.rx_fast_forest](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-forest)  | Floresta aleatória. |
|[microsoftml.rx_fast_linear](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-linear) | Modelo linear. com coordenada dupla Alheatória. |
|[microsoftml.rx_fast_trees](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-trees) | Árvores aumentadas. |
|[microsoftml.rx_logistic_regression](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-logistic-regression) | Regressão logística. |
|[microsoftml.rx_neural_network](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-neural-network) | Rede neural. |
|[microsoftml.rx_oneclass_svm](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-oneclass-svm) | Detecção de anomalias. |

<a name="ml-transforms"></a>

## <a name="2-transform-functions"></a>Funções de transformação 2

### <a name="categorical-variable-handling"></a>Tratamento de variável categórico

| Função | Descrição |
|----------|-------------|
|[microsoftml.categorical](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical) | Converte uma coluna de texto em categorias. |
|[microsoftml.categorical_hash](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical-hash) | Hashes e converte uma coluna de texto em categorias. |

### <a name="schema-manipulation"></a>Manipulação de esquema

| Função | Descrição |
|----------|-------------|
|[microsoftml.concat](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/concat) | Concatena várias colunas em um vetor simples. |
|[microsoftml.drop_columns](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/drop-columns) | Descarta colunas de um conjunto de dados. |
|[microsoftml.select_columns](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/select-columns) | Retém as colunas de um conjunto de dados. |


### <a name="variable-selection"></a>Seleção de variáveis

| Função | Descrição |
|----------|-------------|
|[microsoftml.count_select](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/count-select) |Seleção de recursos com base na contagem. |
|[microsoftml.mutualinformation_select](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/mutualinformation-select) | Seleção de recursos com base em informações mútuas. |


### <a name="text-analytics"></a>Análise de texto

| Função | Descrição |
|----------|-------------|
|[microsoftml.featurize_text](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/featurize-text) | Converte colunas de texto em recursos numéricos. |
|[microsoftml.get_sentiment](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/get-sentiment) | Análise de sentimento. |


### <a name="image-analytics"></a>Análise de imagens 

| Função | Descrição |
|----------|-------------|
|[microsoftml.load_image](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/load-image) | Carrega uma imagem. |
|[microsoftml.resize_image](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/resize-image) | Redimensiona uma imagem. |
|[microsoftml.extract_pixels](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/extract-pixels) | Extrai os pixels de uma imagem. |
|[microsoftml.featurize_image](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/featurize-image) | Converte uma imagem em recursos. |

### <a name="featurization-functions"></a>Funções de personalização

| Função | Descrição |
|----------|-------------|
|[microsoftml.rx_featurize](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-featurize) | Transformação de dados para fontes de dados |

<a name="ml-scoring"></a>

## <a name="3-scoring-functions"></a>Funções de pontuação de 3

| Função | Descrição |
|----------|-------------|
|[microsoftml.rx_predict](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-predict) | Pontuações usando um modelo de aprendizado de máquina da Microsoft |

## <a name="how-to-call-microsoftml"></a>Como chamar microsoftml

Funções em **microsoftml** podem ser chamados no código do Python encapsulado em procedimentos armazenados. A maioria dos desenvolvedores construir **microsoftml** localmente, soluções e, em seguida, migrar o código do Python concluído para procedimentos armazenados como um exercício de implantação.

O **microsoftml** para o Python é instalado por padrão, mas ao contrário do pacote **revoscalepy**, ele não será carregado por padrão quando você inicia uma sessão de Python usando os executáveis do Python instalados com o SQL Server.

Como uma primeira etapa, importe as **microsoftml** de pacote e, em seguida, importe **revoscalepy** se você precisa usar contextos de computação remota ou objetos de fonte de dados ou conectividade relacionados. Em seguida, fazer referência a funções individuais que você precisa.

```python
from microsoftml.modules.logistic_regression.rx_logistic_regression import rx_logistic_regression
from revoscalepy.functions.RxSummary import rx_summary
from revoscalepy.etl.RxImport import rx_import_datasource
```

## <a name="see-also"></a>Confira também

+ [Tutoriais do Python](../tutorials/sql-server-python-tutorials.md)
+ [Tutorial: Incorporar código Python no T-SQL](../tutorials/run-python-using-t-sql.md)
+ [Referência de Python (Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference)

