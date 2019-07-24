---
title: Início rápido para trabalhar com estruturas de dados em Python
description: Neste guia de início rápido para o script Python no SQL Server, saiba como usar estruturas de dados com o procedimento armazenado do sistema sp_execute_external_script.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
ms.openlocfilehash: 0d841314bd2bf167c4c40f5786a116b7bc8f73c0
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344557"
---
# <a name="quickstart-python-data-structures-in-sql-server"></a>Início Rápido: Estruturas de dados do Python no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este guia de início rápido mostra como usar estruturas de dados ao usar o Python no SQL Server Serviços de Machine Learning.

SQL Server se baseia no pacote do  Python pandas, que é ótimo para trabalhar com dados tabulares. No entanto, você não pode passar um escalar do Python para SQL Server e esperar que ele "simplesmente funcione". Neste guia de início rápido, examinaremos algumas definições básicas de tipo de dados, para prepará-lo para problemas adicionais que você possa encontrar ao passar dados tabulares entre Python e SQL Server.

+ Um quadro de dados é uma tabela com _várias_ colunas.
+ Uma única coluna de um dataframe é um objeto do tipo lista chamado série.
+ Um único valor é uma célula de um quadro de dados e deve ser chamado pelo índice.

Como você exporia o único resultado de um cálculo como um quadro de dados, se um data. frame exigir uma estrutura de tabela? Uma resposta é representar o valor escalar único como uma série, que é facilmente convertida em um quadro de dados. 

## <a name="prerequisites"></a>Pré-requisitos

Um guia de início rápido anterior, [Verifique se o Python existe no SQL Server](quickstart-python-verify.md), fornece informações e links para configurar o ambiente do Python necessário para este guia de início rápido.

## <a name="scalar-value-as-a-series"></a>Valor escalar como uma série

Este exemplo faz uma matemática simples e converte um escalar em uma série.

1. Uma série requer um índice, que você pode atribuir manualmente, como mostrado aqui ou programaticamente.

    ```sql
    execute sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    a = 1
    b = 2
    c = a/b
    print(c)
    s = pandas.Series(c, index =["simple math example 1"])
    print(s)
    '
    ```

2. Como a série não foi convertida em um data. frame, os valores são retornados na janela mensagens, mas você pode ver que os resultados estão em um formato de tabela mais.

    **Resultados**

    ```text
    STDOUT message(s) from external script: 
    0.5
    simple math example 1    0.5
    dtype: float64
    ```

3. Para aumentar o tamanho da série, você pode adicionar novos valores usando uma matriz. 

    ```sql
    execute sp_execute_external_script 
    @language = N'Python', 
    @script = N'
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

4. Se você aumentar o número de valores de **índice** , mas não adicionar novos valores de **dados** , os valores de dados serão repetidos para preencher a série.

    ```sql
    execute sp_execute_external_script 
    @language = N'Python', 
    @script = N'
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

Depois de converter nossos resultados de matemática escalar em uma estrutura tabular, ainda precisamos convertê-los em um formato que SQL Server possa manipular. 

1. Para converter uma série em um data. frame, chame o método pandas [dataframe](https://pandas.pydata.org/pandas-docs/stable/dsintro.html#dataframe) .

    ```sql
    execute sp_execute_external_script 
    @language = N'Python', 
    @script = N'
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
    WITH RESULT SETS (( ResultValue float ))
    ```

2. O resultado é mostrado abaixo. Mesmo que você use o índice para obter valores específicos do Data. frame, os valores de índice não fazem parte da saída.

    **Resultados**

    |Resultadovalue|
    |------|
    |0.5|
    |2|

## <a name="output-values-into-dataframe"></a>Valores de saída em data. frame

Vamos ver como a conversão para um data. frame funciona com nossas duas séries que contêm os resultados de operações matemáticas simples. O primeiro tem um índice de valores sequenciais gerados pelo Python. O segundo usa um índice arbitrário de valores de cadeia de caracteres.

1. Este exemplo obtém um valor da série que usa um índice de número inteiro.

    ```sql
    EXECUTE sp_execute_external_script 
    @language = N'Python', 
    @script = N'
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
    WITH RESULT SETS (( ResultValue float ))
    ```

    Lembre-se de que o índice gerado automaticamente começa em 0. Tente usar um valor de índice fora do intervalo e veja o que acontece.

2. Agora, vamos obter um único valor do outro quadro de dados que tem um índice de cadeia de caracteres. 

    ```sql
    EXECUTE sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    import pandas as pd
    a = 1
    b = 2
    c = a/b
    s = pandas.Series(c, index =["simple math example 1", "simple math example 2"])
    print(s)
    df = pd.DataFrame(s, index=["simple math example 1"])
    OutputDataSet = df
    '
    WITH RESULT SETS (( ResultValue float ))
    ```

    **Resultados**

    |Resultadovalue|
    |------|
    |0.5|

    Se você tentar usar um índice numérico para obter um valor dessa série, obterá um erro.

## <a name="next-steps"></a>Próximas etapas

Em seguida, você criará um modelo de previsão usando Python em SQL Server.

> [!div class="nextstepaction"]
> [Criar, treinar e usar um modelo Python com procedimentos armazenados no SQL Server](quickstart-python-train-score-in-tsql.md)