---
title: Pacote microsoftml do Python
description: O microsoftml é um pacote de Python da Microsoft que fornece algoritmos de machine learning de alto desempenho. Ele inclui funções para treinamento e transformações, pontuação, análise de texto e imagem e extração de recursos para obtenção de valores dos dados existentes. O pacote está incluído nos Serviços de Machine Learning do SQL Server.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 07/14/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: ae408162ada9b43a9601c4058b9850db5a4afec4
ms.sourcegitcommit: d1535944bff3f2580070cc036ece30f1d43ee2ce
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2020
ms.locfileid: "86406189"
---
# <a name="microsoftml-python-package-in-sql-server-machine-learning-services"></a>microsoftml (pacote de Python nos Serviços de Machine Learning do SQL Server)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

O **microsoftml** é um pacote de Python da Microsoft que fornece algoritmos de machine learning de alto desempenho. Ele inclui funções para treinamento e transformações, pontuação, análise de texto e imagem e extração de recursos para obtenção de valores dos dados existentes. O pacote está incluído nos [Serviços de Machine Learning do SQL Server](../sql-server-machine-learning-services.md) e dá suporte ao alto desempenho em Big Data usando o processamento de vários núcleos e o streaming de dados rápido.

## <a name="full-reference-documentation"></a>Documentação de referência completa

O pacote **microsoftml** é distribuído em vários produtos da Microsoft, mas o uso é o mesmo com o pacote no SQL Server ou em outro produto. Como as funções são as mesmas, a [documentação para funções individuais do microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) é publicada em apenas uma localização na [referência do R](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference) para o Microsoft Machine Learning Server. Se existirem comportamentos específicos do produto, as discrepâncias serão indicadas na página de ajuda da função.

## <a name="versions-and-platforms"></a>Versões e plataformas

O módulo **microsoftml** se baseia no Python 3.5 e está disponível somente quando você instala um dos seguintes produtos ou downloads da Microsoft:

+ [Serviços de Machine Learning do SQL Server](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 ou posterior](https://docs.microsoft.com/machine-learning-server/)
+ [Bibliotecas de clientes do Python para um cliente de ciência de dados](setup-python-client-tools-sql.md)

> [!NOTE]
> As versões completas do produto são somente Windows no SQL Server 2017. Há suporte no Windows e no Linux para o **microsoftml** no [SQL Server 2019](../../linux/sql-server-linux-setup-machine-learning.md).

## <a name="package-dependencies"></a>Dependências do pacote

Os algoritmos do **microsoftml** dependem do [revoscalepy](ref-py-revoscalepy.md) para:

+ Objetos de fonte de dados. Os dados consumidos pelas funções do **microsoftml** são criados usando funções do **revoscalepy**.
+ Computação remota (mudança da execução da função para uma instância remota do SQL Server). O pacote **revoscalepy** fornece funções para criar e ativar um contexto de computação remota para o SQL Server.

Na maioria dos casos, você carregará os pacotes juntos sempre que estiver usando o **microsoftml**.

## <a name="functions-by-category"></a>Funções por categoria

Esta seção lista as funções por categoria para dar uma ideia de como cada uma é usada. Use também o [sumário](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference) para localizar as funções em ordem alfabética.

## <a name="1-training-functions"></a>1 – Funções de treinamento

| Função | Descrição |
|----------|-------------|
|[microsoftml.rx_ensemble](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-ensemble) | Treine um ensemble de modelos. |
|[microsoftml.rx_fast_forest](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-forest)  | Floresta aleatória. |
|[microsoftml.rx_fast_linear](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-linear) | Modelo linear. com o Ascendente de Coordenada Dupla Alheatória. |
|[microsoftml.rx_fast_trees](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-fast-trees) | Árvores aumentadas. |
|[microsoftml.rx_logistic_regression](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-logistic-regression) | Regressão logística. |
|[microsoftml.rx_neural_network](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-neural-network) | Rede neural. |
|[microsoftml.rx_oneclass_svm](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-oneclass-svm) | Detecção de anomalias. |

<a name="ml-transforms"></a>

## <a name="2-transform-functions"></a>2 – Funções de transformação

### <a name="categorical-variable-handling"></a>Tratamento de variável categórica

| Função | Descrição |
|----------|-------------|
|[microsoftml.categorical](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical) | Converte uma coluna de texto em categorias. |
|[microsoftml.categorical_hash](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/categorical-hash) | Realiza hash e converte uma coluna de texto em categorias. |

### <a name="schema-manipulation"></a>Manipulação de esquema

| Função | Descrição |
|----------|-------------|
|[microsoftml.concat](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/concat) | Concatena várias colunas em um único vetor. |
|[microsoftml.drop_columns](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/drop-columns) | Remove colunas de um conjunto de dados. |
|[microsoftml.select_columns](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/select-columns) | Retém colunas de um conjunto de dados. |


### <a name="variable-selection"></a>Seleção de variáveis

| Função | Descrição |
|----------|-------------|
|[microsoftml.count_select](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/count-select) |Seleção de recursos com base em contagens. |
|[microsoftml.mutualinformation_select](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/mutualinformation-select) | Seleção de recursos com base em informações mútuas. |


### <a name="text-analytics"></a>Análise de Texto

| Função | Descrição |
|----------|-------------|
|[microsoftml.featurize_text](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/featurize-text) | Converte as colunas de texto em recursos numéricos. |
|[microsoftml.get_sentiment](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/get-sentiment) | Análise de sentimento. |


### <a name="image-analytics"></a>Análise de imagem 

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

## <a name="3-scoring-functions"></a>3 – Funções de pontuação

| Função | Descrição |
|----------|-------------|
|[microsoftml.rx_predict](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/rx-predict) | Pontuações usando um modelo de machine learning da Microsoft |

## <a name="how-to-call-microsoftml"></a>Como chamar o microsoftml

As funções do **microsoftml** podem ser chamadas no código Python encapsulado em procedimentos armazenados. A maioria dos desenvolvedores cria soluções do **microsoftml** localmente e, em seguida, migra o código do Python concluído para procedimentos armazenados como um exercício de implantação.

O pacote **microsoftml** para o Python está instalado por padrão, mas, ao contrário do **revoscalepy**, ele não é carregado por padrão quando você inicia uma sessão do Python usando os executáveis do Python instalados com o SQL Server.

Como uma primeira etapa, importe o pacote **microsoftml** e importe o **revoscalepy** caso precise usar contextos de computação remota ou objetos de fonte de dados ou conectividade relacionados. Em seguida, faça referência às funções individuais de que você precisa.

```python
from microsoftml.modules.logistic_regression.rx_logistic_regression import rx_logistic_regression
from revoscalepy.functions.RxSummary import rx_summary
from revoscalepy.etl.RxImport import rx_import_datasource
```

## <a name="see-also"></a>Confira também

+ [Tutoriais do Python](../tutorials/sql-server-python-tutorials.md)
+ [Referência do Python (Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference)

