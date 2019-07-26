---
title: pacote microsoftml Python
description: Apresenta os algoritmos e modelos do Microsoft Machine Learning para Python, conforme relacionado a cargas de trabalho de SQL Server Machine Learning.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/04/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: c2d27b295df6b29d69ce90a7c70c135a197b68b0
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470230"
---
# <a name="microsoftml-python-module-in-sql-server"></a>microsoftml (módulo python no SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**microsoftml** é um módulo compatível com Python35 da Microsoft que fornece algoritmos de aprendizado de máquina de alto desempenho. Ele inclui funções para treinamento e transformações, pontuação, análise de texto e imagem e extração de recursos para derivar valores de dados existentes.

As APIs de Machine Learning foram desenvolvidas pela Microsoft para aplicativos de aprendizado de máquina internos e foram refinadas ao longo dos anos para dar suporte a alto desempenho em Big Data, usando processamento de vários núcleos e streaming de dados rápido. Esse pacote foi originado como um equivalente em Python de uma versão de R, [MicrosoftML](../r/ref-r-microsoftml.md), que tem funções semelhantes. 

## <a name="full-reference-documentation"></a>Documentação de referência completa

A biblioteca **microsoftml** é distribuída em vários produtos da Microsoft, mas o uso é o mesmo se você obter a biblioteca em SQL Server ou em outro produto. Como as funções são as mesmas, a [documentação para funções individuais microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) é publicada em apenas um local sob a [referência do Python](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference) para Microsoft Machine Learning Server. Se existirem comportamentos específicos do produto, as discrepâncias serão indicadas na página de ajuda da função.

## <a name="versions-and-platforms"></a>Versões e plataformas

O módulo **microsoftml** se baseia no Python 3,5 e está disponível somente quando você instala um dos seguintes produtos ou downloads da Microsoft:

+ [SQL Server 2017 Serviços de Machine Learning](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 ou posterior](https://docs.microsoft.com/machine-learning-server/)
+ [Bibliotecas de cliente Python para um cliente de ciência de dados](setup-python-client-tools-sql.md)

> [!NOTE]
> As versões completas de lançamento do produto são somente Windows, a partir do SQL Server 2017. O suporte do Linux para **microsoftml** é novo na versão [prévia do SQL Server 2019](../../linux/sql-server-linux-setup-machine-learning.md).

## <a name="package-dependencies"></a>Dependências do pacote

Os algoritmos no **microsoftml** dependem do [revoscalepy](ref-py-revoscalepy.md) para:

+ Objetos de fonte de dados. Os dados consumidos pelas funções **microsoftml** são criados usando as funções **revoscalepy** .
+ Computação remota (mudança da execução da função para uma instância de SQL Server remota). A biblioteca **revoscalepy** fornece funções para criar e ativar um contexto de computação remota para o SQL Server.

Na maioria dos casos, você carregará os pacotes ao mesmo tempo em que estiver usando o **microsoftml**.

## <a name="functions-by-category"></a>Funções por categoria

Esta seção lista as funções por categoria para dar uma ideia de como cada uma é usada. Você também pode [usar o Sumário](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference) para localizar funções em ordem alfabética.

## <a name="1-training-functions"></a>1-funções de treinamento

| Função | Descrição |
|----------|-------------|
|[microsoftml.rx_ensemble](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-ensemble) | Treine um Ensemble de modelos. |
|[microsoftml.rx_fast_forest](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-forest)  | Floresta aleatória. |
|[microsoftml.rx_fast_linear](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-linear) | Modelo linear. com a coordenada de estocástico dupla ascendente. |
|[microsoftml.rx_fast_trees](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-trees) | Árvores aumentadas. |
|[microsoftml.rx_logistic_regression](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-logistic-regression) | Regressão logística. |
|[microsoftml.rx_neural_network](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-neural-network) | Rede neural. |
|[microsoftml.rx_oneclass_svm](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-oneclass-svm) | Detecção de anomalias. |

<a name="ml-transforms"></a>

## <a name="2-transform-functions"></a>2-funções de transformação

### <a name="categorical-variable-handling"></a>Manipulação de variável categórica

| Função | Descrição |
|----------|-------------|
|[microsoftml.categorical](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical) | Converte uma coluna de texto em categorias. |
|[microsoftml.categorical_hash](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical-hash) | Aplica hash e converte uma coluna de texto em categorias. |

### <a name="schema-manipulation"></a>Manipulação de esquema

| Função | Descrição |
|----------|-------------|
|[microsoftml.concat](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/concat) | Concatena várias colunas em um único vetor. |
|[microsoftml.drop_columns](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/drop-columns) | Remove colunas de um DataSet. |
|[microsoftml.select_columns](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/select-columns) | Retém colunas de um DataSet. |


### <a name="variable-selection"></a>Seleção de variáveis

| Função | Descrição |
|----------|-------------|
|[microsoftml.count_select](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/count-select) |Seleção de recursos com base em contagens. |
|[microsoftml.mutualinformation_select](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/mutualinformation-select) | Seleção de recursos com base em informações mútuas. |


### <a name="text-analytics"></a>Análise de texto

| Função | Descrição |
|----------|-------------|
|[microsoftml.featurize_text](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/featurize-text) | Converte as colunas de texto em recursos numéricos. |
|[microsoftml.get_sentiment](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/get-sentiment) | Análise de sentimentos. |


### <a name="image-analytics"></a>Análise de imagem 

| Função | Descrição |
|----------|-------------|
|[microsoftml.load_image](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/load-image) | Carrega uma imagem. |
|[microsoftml.resize_image](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/resize-image) | Redimensiona uma imagem. |
|[microsoftml.extract_pixels](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/extract-pixels) | Extrai pixels de uma imagem. |
|[microsoftml.featurize_image](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/featurize-image) | Converte uma imagem em recursos. |

### <a name="featurization-functions"></a>Funções personalização

| Função | Descrição |
|----------|-------------|
|[microsoftml.rx_featurize](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-featurize) | Transformação de dados para fontes de dados |

<a name="ml-scoring"></a>

## <a name="3-scoring-functions"></a>3-funções de Pontuação

| Função | Descrição |
|----------|-------------|
|[microsoftml.rx_predict](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-predict) | Pontuações usando um modelo do Microsoft Machine Learning |

## <a name="how-to-call-microsoftml"></a>Como chamar microsoftml

As funções no **microsoftml** são chamáveis no código Python encapsulado em procedimentos armazenados. A maioria dos desenvolvedores cria soluções **microsoftml** localmente e, em seguida, migra o código Python concluído para procedimentos armazenados como um exercício de implantação.

O pacote **microsoftml** para Python é instalado por padrão, mas ao contrário de **revoscalepy**, ele não é carregado por padrão quando você inicia uma sessão do Python usando os executáveis do python instalados com o SQL Server.

Como uma primeira etapa, importe o pacote **microsoftml** e importe **revoscalepy** se precisar usar contextos de computação remota ou objetos de fonte de dados ou conectividade relacionados. Em seguida, referencie as funções individuais de que você precisa.

```python
from microsoftml.modules.logistic_regression.rx_logistic_regression import rx_logistic_regression
from revoscalepy.functions.RxSummary import rx_summary
from revoscalepy.etl.RxImport import rx_import_datasource
```

## <a name="see-also"></a>Confira também

+ [Tutoriais do Python](../tutorials/sql-server-python-tutorials.md)
+ [Tutorial: Inserir código Python no T-SQL](../tutorials/run-python-using-t-sql.md)
+ [Referência do Python (Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference)

