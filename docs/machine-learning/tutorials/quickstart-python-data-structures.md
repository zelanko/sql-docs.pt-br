---
title: 'Início Rápido: estruturas de dados do Python'
titleSuffix: SQL machine learning
description: Neste início rápido, saiba como trabalhar com estrutura de dados e objetos de dados no Python usando o machine learning do SQL.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/28/2020
ms.topic: quickstart
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: 1ad1aba8a87e5668949f3e7810f0ee6066932171
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94870143"
---
# <a name="quickstart-data-structures-and-objects-using-python-with-sql-machine-learning"></a>Início Rápido: Estruturas de dados e objetos usando o Python com o machine learning do SQL
[!INCLUDE [SQL Server 2017 SQL MI](../../includes/applies-to-version/sqlserver2017-asdbmi.md)]

Neste início rápido, você aprenderá a usar estruturas e tipos de dados ao usar Python nos [Serviços de Machine Learning do SQL Server](../sql-server-machine-learning-services.md), nos [Serviços de Machine Learning da Instância Gerenciada de SQL do Azure](/azure/azure-sql/managed-instance/machine-learning-services-overview) ou nos [Clusters de Big Data do SQL Server](../../big-data-cluster/machine-learning-services.md). Você aprenderá como mover dados entre o Python e o SQL Server e os problemas comuns que podem ocorrer.

O machine learning do SQL se baseia no pacote **Pandas** do Python, que é ótimo para trabalhar usando dados tabulares. No entanto, você não pode passar um escalar do Python para o seu banco de dados e esperar que ele *simplesmente funcione*. Neste início rápido, você examinará algumas definições básicas de estrutura de dados, a fim de se preparar para problemas adicionais que pode enfrentar ao passar dados tabulares entre o Python e o banco de dados.

Os conceitos que se deve conhecer de antemão incluem:

- Uma estrutura de dados é uma tabela com _várias_ colunas.
- Uma coluna única de uma estrutura de dados é um objeto semelhante a uma lista, chamado série.
- Um valor único de uma estrutura de dados é chamado de célula e é acessado pelo índice.

Como você faria para expor o único resultado de um cálculo como uma estrutura de dados, se uma variável data.frame exigisse uma estrutura de tabela? Uma resposta possível é representar o valor escalar único como uma série, que pode ser convertida facilmente em uma estrutura de dados.

> [!NOTE]
> Ao retornar datas, o Python no SQL usa DATETIME, que tem um intervalo de datas restrito de 1753-01-01(-53690) a 9999-12-31 (2958463).

## <a name="prerequisites"></a>Pré-requisitos

Para executar este início rápido, você precisará dos pré-requisitos a seguir.

- Um banco de dados SQL em uma destas plataformas:
  - [Serviços de Machine Learning do SQL Server](../sql-server-machine-learning-services.md). Para instalá-lo, confira o [Guia de instalação do Windows](../install/sql-machine-learning-services-windows-install.md) ou o [Guia de instalação do Linux](../../linux/sql-server-linux-setup-machine-learning.md?toc=%2Fsql%2Fmachine-learning%2Ftoc.json).
  - Clusters de Big Data do SQL Server. Veja como [habilitar os Serviços de Machine Learning em Clusters de Big Data do SQL Server](../../big-data-cluster/machine-learning-services.md).
  - Serviços de Machine Learning da Instância Gerenciada de SQL do Azure. Para obter informações, confira a [Visão geral dos Serviços de Machine Learning da Instância Gerenciada de SQL do Azure](/azure/azure-sql/managed-instance/machine-learning-services-overview).

- Uma ferramenta para executar consultas SQL que contenham scripts Python. Este início rápido usa o [Azure Data Studio](../../azure-data-studio/what-is.md).

## <a name="scalar-value-as-a-series"></a>Valor escalar como uma série

Este exemplo usa um pouco de matemática simples e converte um escalar em uma série.

1. Uma série requer um índice, que pode ser atribuído manualmente por você, conforme mostrado aqui, bem como programaticamente.

   ```sql
   EXECUTE sp_execute_external_script @language = N'Python'
       , @script = N'
   a = 1
   b = 2
   c = a/b
   print(c)
   s = pandas.Series(c, index =["simple math example 1"])
   print(s)
   '
   ```

   Já que a série não foi convertida em uma data.frame, os valores são retornados na janela mensagens, mas você pode ver que os resultados estão em um formato mais tabular.

   **Resultados**

   ```text
   STDOUT message(s) from external script: 
   0.5
   simple math example 1    0.5
   dtype: float64
   ```

1. Para aumentar o tamanho da série, você pode adicionar novos valores usando uma matriz.

   ```sql
   EXECUTE sp_execute_external_script @language = N'Python'
       , @script = N'
   a = 1
   b = 2
   c = a/b
   d = a*b
   s = pandas.Series([c,d])
   print(s)
   '
   ```

   Caso você não especifique um índice, um será gerado, com valores começando com 0 e terminando com o tamanho da matriz.

   **Resultados**

   ```text
   STDOUT message(s) from external script:
   0    0.5
   1    2.0
   dtype: float64
   ```

1. Se você aumentar o número de valores de **índice** mas não adicionar novos valores de **dados**, os valores de dados serão repetidos para preencher a série.

   ```sql
   EXECUTE sp_execute_external_script @language = N'Python'
       , @script = N'
   a = 1
   b = 2
   c = a/b
   s = pandas.Series(c, index =["simple math example 1", "simple math example 2"])
   print(s)
   '
   ```

   **Resultados**

   ```text
   STDOUT message(s) from external script:
   0.5
   simple math example 1    0.5
   simple math example 2    0.5
   dtype: float64
   ```

## <a name="convert-series-to-data-frame"></a>Converter série em estrutura de dados

Depois de converter os resultados de matemática escalar em uma estrutura de tabela, você ainda precisa convertê-los em um formato que o machine learning do SQL possa manipular.

1. Para converter uma série em um data.frame, chame o método [DataFrame](https://pandas.pydata.org/pandas-docs/stable/dsintro.html#dataframe) do Pandas.

   ```sql
   EXECUTE sp_execute_external_script @language = N'Python'
       , @script = N'
   import pandas as pd
   a = 1
   b = 2
   c = a/b
   d = a*b
   s = pandas.Series([c,d])
   print(s)
   df = pd.DataFrame(s)
   OutputDataSet = df
   '
   WITH RESULT SETS((ResultValue FLOAT))
   ```

   O resultado é mostrado abaixo. Mesmo que você use o índice para obter valores específicos do data.frame, os valores de índice não fazem parte da saída.

   **Resultados**

   |ResultValue|
   |------|
   |0.5|
   |2|

## <a name="output-values-into-dataframe"></a>Valores de saída em data.frame

Agora, você produzirá valores específicos de duas séries de resultados matemáticos em um data.frame. A primeira tem um índice de valores sequenciais gerados pelo Python. A segunda usa um índice arbitrário de valores de cadeia de caracteres.

1. O exemplo a seguir obtém um valor da série usando um índice de número inteiro.

   ```sql
   EXECUTE sp_execute_external_script @language = N'Python'
       , @script = N'
   import pandas as pd
   a = 1
   b = 2
   c = a/b
   d = a*b
   s = pandas.Series([c,d])
   print(s)
   df = pd.DataFrame(s, index=[1])
   OutputDataSet = df
   '
   WITH RESULT SETS((ResultValue FLOAT))
   ```

   **Resultados**

   |ResultValue|
   |------|
   |2,0|

   Lembre-se de que o índice gerado automaticamente começa em 0. Tente usar um valor de índice fora do intervalo e veja o que acontece.

1. Agora, obtenha um único valor da outra estrutura de dados usando um índice de cadeia de caracteres.

   ```sql
   EXECUTE sp_execute_external_script @language = N'Python'
       , @script = N'
   import pandas as pd
   a = 1
   b = 2
   c = a/b
   s = pandas.Series(c, index =["simple math example 1", "simple math example 2"])
   print(s)
   df = pd.DataFrame(s, index=["simple math example 1"])
   OutputDataSet = df
   '
   WITH RESULT SETS((ResultValue FLOAT))
   ```

   **Resultados**

   |ResultValue|
   |------|
   |0.5|

   Se você tentar usar um índice numérico para obter um valor dessa série, obterá um erro.

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre como escrever funções avançadas do Python com o machine learning do SQL, siga este início rápido:

> [!div class="nextstepaction"]
> [Escrever funções avançadas de Python](quickstart-python-functions.md)
