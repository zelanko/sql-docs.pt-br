---
title: Trabalhar com tipos e objetos de dados do Python e do SQL
titleSuffix: SQL Server Machine Learning Services
description: Neste guia de início rápido, saiba como trabalhar com tipos de dados e objetos de dados no Python e SQL Server com SQL Server Serviços de Machine Learning.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/17/2019
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e3606072fefa9b74adcfdb914d02e4e82c11e0eb
ms.sourcegitcommit: 9221a693d4ab7ae0a7e2ddeb03bd0cf740628fd0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/23/2019
ms.locfileid: "71199438"
---
# <a name="quickstart-handle-data-types-and-objects-using-python-in-sql-server-machine-learning-services"></a>Início Rápido: Manipular tipos de dados e objetos usando Python no SQL Server Serviços de Machine Learning
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este guia de início rápido mostra como usar estruturas de dados ao usar o Python no SQL Server Serviços de Machine Learning.

SQL Server se baseia no pacote do Python pandas, que é ótimo para trabalhar com dados tabulares. No entanto, você não pode passar um escalar do Python para SQL Server e esperar que ele "simplesmente funcione". Neste guia de início rápido, você examinará algumas definições básicas de tipo de dados, para prepará-lo para problemas adicionais que você possa encontrar ao passar dados tabulares entre Python e SQL Server.

Conceitos para conhecer o front include:

+ Um quadro de dados é uma tabela com _várias_ colunas.
+ Uma única coluna de um quadro de dados é um objeto como uma lista chamado série.
+ Um único valor de um quadro de dados é chamado de uma célula e é acessado pelo índice.

Como você exporia o único resultado de um cálculo como um quadro de dados, se um data. frame exigir uma estrutura de tabela? Uma resposta é representar o valor escalar único como uma série, que é facilmente convertida em um quadro de dados. 

## <a name="prerequisites"></a>Pré-requisitos

- Este início rápido requer acesso a uma instância do SQL Server com [SQL Server serviços de Machine Learning](../install/sql-machine-learning-services-windows-install.md) com a linguagem Python instalada.

- Você também precisa de uma ferramenta para executar consultas SQL que contêm scripts Python. Você pode executar esses scripts usando qualquer ferramenta de consulta ou gerenciamento de banco de dados, desde que ele possa se conectar a uma instância de SQL Server e executar uma consulta T-SQL ou um procedimento armazenado. Este início rápido usa o [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms).

## <a name="scalar-value-as-a-series"></a>Valor escalar como uma série

Este exemplo faz uma matemática simples e converte um escalar em uma série.

1. Uma série requer um índice, que você pode atribuir manualmente, como mostrado aqui ou programaticamente.

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

   Como a série não foi convertida em um data. frame, os valores são retornados na janela mensagens, mas você pode ver que os resultados estão em um formato de tabela mais.

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

   Se você não especificar um índice, será gerado um índice com valores começando com 0 e terminando com o comprimento da matriz.

   **Resultados**

   ```text
   STDOUT message(s) from external script: 
   0    0.5
   1    2.0
   dtype: float64
   ```

1. Se você aumentar o número de valores de **índice** , mas não adicionar novos valores de **dados** , os valores de dados serão repetidos para preencher a série.

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

## <a name="convert-series-to-data-frame"></a>Converter série em quadro de dados

Depois de converter os resultados de matemática escalar em uma estrutura de tabela, você ainda precisa convertê-los em um formato que SQL Server possa manipular.

1. Para converter uma série em um data. frame, chame o método pandas [dataframe](https://pandas.pydata.org/pandas-docs/stable/dsintro.html#dataframe) .

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

   O resultado é mostrado abaixo. Mesmo que você use o índice para obter valores específicos do Data. frame, os valores de índice não fazem parte da saída.

   **Resultados**

   |Resultadovalue|
   |------|
   |0,5|
   |2|

## <a name="output-values-into-dataframe"></a>Valores de saída em data. frame

Agora, você produzirá valores específicos de duas séries de resultados matemáticos em um data. frame. O primeiro tem um índice de valores sequenciais gerados pelo Python. O segundo usa um índice arbitrário de valores de cadeia de caracteres.

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

   |Resultadovalue|
   |------|
   |2.0|

   Lembre-se de que o índice gerado automaticamente começa em 0. Tente usar um valor de índice fora do intervalo e veja o que acontece.

1. Agora, obtenha um único valor do outro quadro de dados usando um índice de cadeia de caracteres.

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

   |Resultadovalue|
   |------|
   |0,5|

   Se você tentar usar um índice numérico para obter um valor dessa série, obterá um erro.

## <a name="next-steps"></a>Próximas etapas

Em seguida, você criará um modelo de previsão usando Python em SQL Server.

> [!div class="nextstepaction"]
> [Criar e pontuar um modelo de previsão no Python](quickstart-python-train-score-model.md)

Para obter mais informações sobre SQL Server Serviços de Machine Learning, consulte:

- [O que é SQL Server Serviços de Machine Learning (Python e R)?](../what-is-sql-server-machine-learning.md)
