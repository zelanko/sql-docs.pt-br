---
title: Guia de início rápido para trabalhar com estruturas de dados em Python – Machine Learning do SQL Server
description: Neste início rápido para o script de Python no SQL Server, saiba como usar estruturas de dados com o procedimento armazenado do sistema de sp_execute_external_script.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
ms.openlocfilehash: ffbbd39c08221db4afa6427626ca618e04617166
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962087"
---
# <a name="quickstart-python-data-structures-in-sql-server"></a>Início Rápido: Estruturas de dados do Python no SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este início rápido mostra como usar as estruturas de dados ao usar o Python em serviços do SQL Server Machine Learning.

SQL Server depende do Python **pandas** pacote, que é ideal para trabalhar com dados tabulares. No entanto, você não pode passar um escalar do Python para o SQL Server e esperar que ele "simplesmente funcionem". Neste início rápido, vamos examinar algumas definições de tipo de dados básico, para se preparar para problemas adicionais que podem ocorrer ao passar dados tabulares entre Python e o SQL Server.

+ Um quadro de dados é uma tabela com _vários_ colunas.
+ Uma única coluna de um DataFrame, é um objeto de lista como chamado de uma série.
+ Um único valor é uma célula de um quadro de dados e deve ser chamado por índice.

Como você poderia expor o resultado de um cálculo como um quadro de dados, se um frame requer uma estrutura tabular? Uma resposta é representar o único valor escalar como uma série, o que é facilmente convertida em um quadro de dados. 

## <a name="prerequisites"></a>Pré-requisitos

Um início rápido anterior, [Python Verifique se existe no SQL Server](quickstart-python-verify.md), fornece informações e links para configurar o ambiente do Python necessário para este início rápido.

## <a name="scalar-value-as-a-series"></a>Valor escalar como uma série

Este exemplo faz alguns cálculos matemáticos simples e converte um escalar em uma série.

1. Uma série requer um índice, que você pode atribuir manualmente, conforme mostrado aqui, ou programaticamente.

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

2. Como a série ainda não foi convertida em um Frame, os valores são retornados na janela de mensagens, mas você pode ver que os resultados estão em um formato tabular mais.

    **Resultados**

    ```text
    STDOUT message(s) from external script: 
    0.5
    simple math example 1    0.5
    dtype: float64
    ```

3. Para aumentar o tamanho da série, você pode adicionar novos valores, usando uma matriz. 

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

    Se você não especificar um índice, um índice é gerado que tenha valores começando com 0 e terminando com o comprimento da matriz.

    **Resultados**

    ```text
    STDOUT message(s) from external script: 
    0    0.5
    1    2.0
    dtype: float64
    ```

4. Se você aumentar o número de **índice** valores, mas não adicionar novas **dados** valores, os valores de dados são repetidos para preencher a série.

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

## <a name="convert-series-to-data-frame"></a>Converter série ao quadro de dados

Ter convertido nossos resultados escalares matemática em uma estrutura tabular, ainda precisamos convertê-los em um formato que pode lidar com os do SQL Server. 

1. Para converter uma série em um Frame, chame os pandas [DataFrame](https://pandas.pydata.org/pandas-docs/stable/dsintro.html#dataframe) método.

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

2. O resultado é mostrado abaixo. Mesmo se você usar o índice para obter valores específicos do Frame, os valores de índice não são parte da saída.

    **Resultados**

    |ResultValue|
    |------|
    |0.5|
    |2|

## <a name="output-values-into-dataframe"></a>Valores de saída em Frame

Vamos ver como a conversão para um Frame funciona com nossas duas séries que contém os resultados de operações matemáticas simples. O primeiro tem um índice de valores sequenciais gerados pelo Python. O segundo usa um índice arbitrário de valores de cadeia de caracteres.

1. Este exemplo obtém um valor da série que usa um índice de inteiro.

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

    Lembre-se de que o índice gerado automaticamente começa em 0. Tente usar uma valor fora do intervalo índice e ver o que acontece.

2. Agora vamos obter um único valor de outra estrutura de dados que tem um índice de cadeia de caracteres. 

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

    |ResultValue|
    |------|
    |0.5|

    Se você tentar usar um índice numérico para obter um valor desta série, você obterá um erro.

## <a name="next-steps"></a>Próximas etapas

Em seguida, você criará um modelo de previsão usando o Python no SQL Server.

> [!div class="nextstepaction"]
> [Criar, treinar e usar um modelo de Python com procedimentos armazenados no SQL Server](quickstart-python-train-score-in-tsql.md)