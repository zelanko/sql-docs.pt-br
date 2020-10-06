---
title: 'Início Rápido: executar scripts do Python'
titleSuffix: SQL machine learning
description: Execute um conjunto de scripts Python simples usando os Serviços de Machine Learning no SQL Server, em Clusters de Big Data ou nas Instâncias Gerenciadas de SQL do Azure. Saiba como usar o procedimento armazenado sp_execute_external_script para executar o script.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/28/2020
ms.topic: quickstart
author: cawrites
ms.author: chadam
ms.reviewer: davidph
ms.custom: contperfq1
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: a2db492306aff5b4980bb97a6f65b93515dbfe1b
ms.sourcegitcommit: b93beb4f03aee2c1971909cb1d15f79cd479a35c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/29/2020
ms.locfileid: "91497824"
---
# <a name="quickstart-run-simple-python-scripts-with-sql-machine-learning"></a>Início Rápido: executar scripts simples do Python com o machine learning do SQL
[!INCLUDE [SQL Server 2017 SQL MI](../../includes/applies-to-version/sqlserver2017-asdbmi.md)]

Neste início rápido, você executará um conjunto de scripts Python simples usando os [Serviços de Machine Learning do SQL Server](../sql-server-machine-learning-services.md), os [Serviços de Machine Learning da Instância Gerenciada de SQL do Azure](/azure/azure-sql/managed-instance/machine-learning-services-overview) ou os [Clusters de Big Data do SQL Server](../../big-data-cluster/machine-learning-services.md). Você aprenderá a usar o procedimento armazenado [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) para executar o script em uma instância do SQL Server.

## <a name="prerequisites"></a>Pré-requisitos

Para executar este início rápido, você precisará dos pré-requisitos a seguir.

- Um banco de dados SQL em uma destas plataformas:
  - [Serviços de Machine Learning do SQL Server](../sql-server-machine-learning-services.md). Para saber como instalar os Serviços de Machine Learning, confira o [Guia de instalação do Windows](../install/sql-machine-learning-services-windows-install.md) ou o [Guia de instalação do Linux](../../linux/sql-server-linux-setup-machine-learning.md?toc=%2Fsql%2Fmachine-learning%2Ftoc.json).
  - Clusters de Big Data do SQL Server. Veja como [habilitar os Serviços de Machine Learning em Clusters de Big Data do SQL Server](../../big-data-cluster/machine-learning-services.md).
  - Serviços de Machine Learning da Instância Gerenciada de SQL do Azure. Para saber como se inscrever, confira a [Visão geral dos Serviços de Machine Learning da Instância Gerenciada de SQL do Azure](/azure/azure-sql/managed-instance/machine-learning-services-overview).

- Uma ferramenta para executar consultas SQL que contenham scripts Python. Este início rápido usa o [Azure Data Studio](../../azure-data-studio/what-is.md).

## <a name="run-a-simple-script"></a>Executar um script simples

Para executar um script Python, você o passará como um argumento para o procedimento armazenado do sistema, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). Esse procedimento armazenado do sistema inicia o runtime do Python no contexto do machine learning do SQL, transmite dados para o Python, gerencia as sessões de usuário do Python com segurança e retorna todos os resultados para o cliente.

Nas etapas seguintes, você executará esse script Python de exemplo em seu banco de dados:

```python
a = 1
b = 2
c = a/b
d = a*b
print(c, d)
```

1. Abra uma nova janela de consulta no **Azure Data Studio** conectado à sua instância SQL.

1. Passe o script Python completo para o procedimento armazenado `sp_execute_external_script`.

   O script é passado por meio do argumento `@script`. Tudo dentro do argumento `@script` deve ser um código Python válido.

    ```sql
    EXECUTE sp_execute_external_script @language = N'Python'
        , @script = N'
    a = 1
    b = 2
    c = a/b
    d = a*b
    print(c, d)
    '
    ```

1. O resultado correto é calculado e a função `print` do Python retorna o resultado para a janela **Mensagens**.

   O resultado deve ser semelhante ao mostrado a seguir.

    **Resultados**

    ```text
    STDOUT message(s) from external script:
    0.5 2
    ```

## <a name="run-a-hello-world-script"></a>Executar um script de Olá, Mundo

Um script de exemplo típico é aquele que apenas gera a cadeia de caracteres "Olá, Mundo". Execute o comando a seguir.

```sql
EXECUTE sp_execute_external_script @language = N'Python'
    , @script = N'OutputDataSet = InputDataSet'
    , @input_data_1 = N'SELECT 1 AS hello'
WITH RESULT SETS(([Hello World] INT));
GO
```

As entradas para o procedimento armazenado `sp_execute_external_script` incluem:

| Entrada | Descrição |
|-|-|
| @language | define a extensão da linguagem a ser chamada, neste caso, Python |
| @script | define os comandos passados para o runtime do Python. Todo o script Python deve ser colocado neste argumento como texto Unicode. Você também pode adicionar texto a uma variável do tipo **nvarchar** e chamar a variável |
| @input_data_1 | dados retornados pela consulta, transmitidos ao runtime do Python, que retorna os dados como uma estrutura de dados |
| WITH RESULT SETS | cláusula que define o esquema da tabela de dados retornada para o machine learning do SQL, adicionando "Olá, Mundo" com o nome da coluna, **int** para o tipo de dados |

O comando gera o seguinte texto:

| Olá, Mundo |
|-------------|
| 1 |

## <a name="use-inputs-and-outputs"></a>Use entradas e saídas

Por padrão, `sp_execute_external_script` aceita um único conjunto de dados como entrada, que normalmente você fornece na forma de uma consulta SQL válida. Em seguida, ele retorna uma única estrutura de dados do Python como saída.

Por enquanto, usaremos as variáveis de entrada e saída padrão de `sp_execute_external_script`: **InputDataSet** e **OutputDataSet**.

1. Crie uma pequena tabela de dados de teste.

    ```sql
    CREATE TABLE PythonTestData (col1 INT NOT NULL)
    
    INSERT INTO PythonTestData
    VALUES (1);
    
    INSERT INTO PythonTestData
    VALUES (10);
    
    INSERT INTO PythonTestData
    VALUES (100);
    GO
    ```

1. Use a instrução `SELECT` para consultar a tabela.
  
    ```sql
    SELECT *
    FROM PythonTestData
    ```

    **Resultados**

    ![Conteúdo da tabela PythonTestData](./media/select-pythontestdata.png)

1. Execute o script Python a seguir. Ele recupera os dados da tabela usando a instrução `SELECT`, passa-os pelo runtime do Python e retorna os dados como uma estrutura de dados. A cláusula `WITH RESULT SETS` define o esquema da tabela de dados retornada para o SQL, adicionando o nome de coluna *NewColName*.

    ```sql
    EXECUTE sp_execute_external_script @language = N'Python'
        , @script = N'OutputDataSet = InputDataSet;'
        , @input_data_1 = N'SELECT * FROM PythonTestData;'
    WITH RESULT SETS(([NewColName] INT NOT NULL));
    ```

    **Resultados**

    ![Saída do script Python que retorna dados de uma tabela](./media/python-output-pythontestdata.png)

1. Agora, altere os nomes das variáveis de entrada e de saída. Os nomes padrão das variáveis de entrada e de saída são **InputDataSet** e **OutputDataSet**, respectivamente. O script a seguir altera os nomes para **SQL_in** e **SQL_out**:

    ```sql
    EXECUTE sp_execute_external_script @language = N'Python'
        , @script = N'SQL_out = SQL_in;'
        , @input_data_1 = N'SELECT 12 as Col;'
        , @input_data_1_name  = N'SQL_in'
        , @output_data_1_name = N'SQL_out'
    WITH RESULT SETS(([NewColName] INT NOT NULL));
    ```

    Observe que o Python diferencia maiúsculas de minúsculas. As variáveis de entrada e saída usadas no script Python (**SQL_out**, **SQL_in**) precisam corresponder aos nomes definidos com `@input_data_1_name` e `@output_data_1_name`, incluindo maiúsculas e minúsculas.

    > [!TIP]
    > Só é possível passar um conjunto de dados de entrada como parâmetro, e você pode retornar apenas um conjunto de dados. No entanto, você pode chamar outros conjuntos de dados no código do Python e retornar saídas de outros tipos, além do conjunto de dados. Você também pode adicionar a palavra-chave OUTPUT a qualquer parâmetro para que ele retorne com os resultados.

1. Você também pode gerar valores usando apenas o script Python sem dados de entrada (`@input_data_1` está definido como em branco).

    O script a seguir gera o texto "Olá" e "mundo".

    ```sql
    EXECUTE sp_execute_external_script @language = N'Python'
        , @script = N'
    import pandas as pd
    mytextvariable = pandas.Series(["hello", " ", "world"]);
    OutputDataSet = pd.DataFrame(mytextvariable);
    '
        , @input_data_1 = N''
    WITH RESULT SETS(([Col1] CHAR(20) NOT NULL));
    ```

    **Resultados**

    ![Resultados da consulta usando @script como entrada](./media/python-data-generated-output.png)

> [!NOTE]
> O Python usa espaços à esquerda para agrupar instruções. Assim, quando o script do Python incorporado abranger várias linhas, como no script anterior, não tente recuar os comandos do Python para colocá-los em linha com os comandos do SQL. Este script, por exemplo, produzirá um erro:
>
> ```sql
> EXECUTE sp_execute_external_script @language = N'Python'
>       , @script = N'
>       import pandas as pd
>       mytextvariable = pandas.Series(["hello", " ", "world"]);
>       OutputDataSet = pd.DataFrame(mytextvariable);
>       '
>       , @input_data_1 = N''
> WITH RESULT SETS(([Col1] CHAR(20) NOT NULL));
> ```

## <a name="check-python-version"></a>Verificar a versão do Python

Se você quiser ver qual versão do Python está instalada no servidor, execute o script a seguir.

```sql
EXECUTE sp_execute_external_script @language = N'Python'
    , @script = N'
import sys
print(sys.version)
'
GO
```

A função `print` do Python retorna a versão para a janela **Mensagens**. Na saída de exemplo abaixo, você pode ver que, nesse caso, a versão 3.5.2 do Python está instalada.

**Resultados**

```text
STDOUT message(s) from external script:
3.5.2 |Continuum Analytics, Inc.| (default, Jul  5 2016, 11:41:13) [MSC v.1900 64 bit (AMD64)]
```

## <a name="list-python-packages"></a>Listar pacotes do Python

A Microsoft fornece vários pacotes do Python pré-instalados com os Serviços de Machine Learning.

Para ver uma lista de quais pacotes do Python estão instalados, incluindo a versão, execute o script a seguir.

```SQL
EXECUTE sp_execute_external_script @language = N'Python'
    , @script = N'
import pkg_resources
import pandas
dists = [str(d) for d in pkg_resources.working_set]
OutputDataSet = pandas.DataFrame(dists)
'
WITH RESULT SETS(([Package] NVARCHAR(max)))
GO
```

A lista é do `pkg_resources.working_set` no Python e retornada para o SQL como uma estrutura de dados.

**Resultados**

:::image type="content" source="media/python-package-list.png" alt-text="Lista de pacotes do Python instalados":::

## <a name="next-steps"></a>Próximas etapas

Para saber como usar estruturas de dados ao usar o Python no aprendizado de máquina do SQL Server, siga este início rápido:

> [!div class="nextstepaction"]
> [Início Rápido: objetos e estruturas de dados usando Python](quickstart-python-data-structures.md)
