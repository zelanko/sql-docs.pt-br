---
title: 'Início Rápido: Executar scripts de R'
titleSuffix: SQL machine learning
description: Execute um conjunto de scripts simples do R com o aprendizado de máquina do SQL. Saiba como usar o procedimento armazenado sp_execute_external_script para executar o script.
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/21/2020
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: a924bca8acf50846f8b14053cc01a6a1a35f1617
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94870368"
---
# <a name="quickstart-run-simple-r-scripts-with-sql-machine-learning"></a>Início Rápido: executar scripts simples do R com o aprendizado de máquina do SQL
[!INCLUDE [SQL Server 2016 SQL MI](../../includes/applies-to-version/sqlserver2016-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
Neste início rápido, você executará um conjunto de scripts simples do R usando os [Serviços de Machine Learning do SQL Server](../sql-server-machine-learning-services.md) ou em [Clusters de Big Data](../../big-data-cluster/machine-learning-services.md). Você aprenderá a usar o procedimento armazenado [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) para executar o script em uma instância do SQL Server.
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
Neste início rápido, você executará um conjunto de scripts R simples usando os [Serviços de Machine Learning do SQL Server](../sql-server-machine-learning-services.md). Você aprenderá a usar o procedimento armazenado [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) para executar o script em uma instância do SQL Server.
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
Neste início rápido, você executará um conjunto de scripts simples do R usando o [SQL Server R Services](../r/sql-server-r-services.md). Você aprenderá a usar o procedimento armazenado [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) para executar o script em uma instância do SQL Server.
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
Neste início rápido, você executará um conjunto de scripts R simples usando os [Serviços de Machine Learning de Instância Gerenciada de SQL do Azure](/azure/azure-sql/managed-instance/machine-learning-services-overview). Você aprenderá a usar o procedimento armazenado [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) para executar o script no banco de dados.
::: moniker-end

## <a name="prerequisites"></a>Pré-requisitos

Para executar este início rápido, você precisará dos pré-requisitos a seguir.

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
- Serviços de Machine Learning do SQL Server. Para instalar os Serviços de Machine Learning, confira o [Guia de instalação do Windows](../install/sql-machine-learning-services-windows-install.md) ou o [Guia de instalação do Linux](../../linux/sql-server-linux-setup-machine-learning.md?toc=%2Fsql%2Fmachine-learning%2Ftoc.json). Você também pode [habilitar Serviços de Machine Learning em Clusters de Big Data do SQL Server](../../big-data-cluster/machine-learning-services.md).
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
- Serviços de Machine Learning do SQL Server. Para instalar os Serviços de Machine Learning, confira o [Guia de instalação do Windows](../install/sql-machine-learning-services-windows-install.md). 
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
- SQL Server 2016 R Services. Para instalar o R Services, confira o [Guia de instalação do Windows](../install/sql-r-services-windows-install.md). 
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
- Serviços de Machine Learning da Instância Gerenciada de SQL do Azure. Para obter informações, confira a [Visão geral dos Serviços de Machine Learning da Instância Gerenciada de SQL do Azure](/azure/azure-sql/managed-instance/machine-learning-services-overview).
::: moniker-end

- Uma ferramenta para executar consultas SQL que contenham scripts do R. Este início rápido usa o [Azure Data Studio](../../azure-data-studio/what-is.md).

## <a name="run-a-simple-script"></a>Executar um script simples

Para executar um script R, você o passará como um argumento para o procedimento armazenado do sistema, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). Esse procedimento armazenado do sistema inicia o runtime de R, transmite dados para R, gerencia as sessões de usuário de R com segurança e retorna todos os resultados para o cliente.

Nas etapas a seguir, você executará este exemplo de script do R:

```r
a <- 1
b <- 2
c <- a/b
d <- a*b
print(c(c, d))
```

1. Abra o **Azure Data Studio** e conecte-se ao servidor.

1. Passe o script R completo para o procedimento armazenado `sp_execute_external_script`.

   O script é passado por meio do argumento `@script`. Tudo dentro do argumento `@script` precisa ser código R válido.

    ```sql
    EXECUTE sp_execute_external_script @language = N'R'
        , @script = N'
    a <- 1
    b <- 2
    c <- a/b
    d <- a*b
    print(c(c, d))
    '
    ```

1. O resultado correto é calculado e a função R `print` retorna o resultado na janela **Mensagens**.

   O resultado deve ser semelhante ao mostrado a seguir.

    **Resultados**

    ```text
    STDOUT message(s) from external script:
    0.5 2
    ```

## <a name="run-a-hello-world-script"></a>Executar um script de Olá, Mundo

Um script de exemplo típico é aquele que apenas gera a cadeia de caracteres "Olá, Mundo". Execute o comando a seguir.

```sql
EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'OutputDataSet<-InputDataSet'
    , @input_data_1 = N'SELECT 1 AS hello'
WITH RESULT SETS(([Hello World] INT));
GO
```

As entradas para o procedimento armazenado `sp_execute_external_script` incluem:

| Entrada | Descrição |
|-|-|
| @language | define a extensão da linguagem a ser chamada, neste caso, R |
| @script | define os comandos passados para o runtime do R. O seu script R inteiro deve ser colocado neste argumento como texto Unicode. Você também pode adicionar texto a uma variável do tipo **nvarchar** e chamar a variável |
| @input_data_1 | dados retornados pela consulta, transmitidos ao runtime do R, que retorna os dados como uma estrutura de dados |
|WITH RESULT SETS | cláusula que define o esquema da tabela de dados retornada, adicionando "Olá, Mundo" como o nome da coluna, **int** como o tipo de dados |

O comando gera o seguinte texto:

| Olá, Mundo |
|-------------|
| 1 |

## <a name="use-inputs-and-outputs"></a>Use entradas e saídas

Por padrão, `sp_execute_external_script` aceita um único conjunto de dados como entrada, que normalmente você fornece na forma de uma consulta SQL válida. Em seguida, ele retorna uma única estrutura de dados do R como saída.

Por enquanto, usaremos as variáveis de entrada e saída padrão de `sp_execute_external_script`: **InputDataSet** e **OutputDataSet**.

1. Crie uma pequena tabela de dados de teste.

    ```sql
    CREATE TABLE RTestData (col1 INT NOT NULL)
    
    INSERT INTO RTestData
    VALUES (1);
    
    INSERT INTO RTestData
    VALUES (10);
    
    INSERT INTO RTestData
    VALUES (100);
    GO
    ```

1. Use a instrução `SELECT` para consultar a tabela.
  
    ```sql
    SELECT *
    FROM RTestData
    ```

    **Resultados**

    ![Conteúdo da tabela RTestData](./media/select-rtestdata.png)

1. Execute o script R a seguir. Ele recupera os dados da tabela usando a instrução `SELECT`, passa-os pelo runtime do R e retorna os dados como uma estrutura de dados. A cláusula `WITH RESULT SETS` define o esquema da tabela de dados retornada para o SQL, adicionando o nome de coluna *NewColName*.

    ```sql
    EXECUTE sp_execute_external_script @language = N'R'
        , @script = N'OutputDataSet <- InputDataSet;'
        , @input_data_1 = N'SELECT * FROM RTestData;'
    WITH RESULT SETS(([NewColName] INT NOT NULL));
    ```

    **Resultados**

    ![Saída do script R que retorna dados de uma tabela](./media/r-output-rtestdata.png)

1. Agora, vamos alterar os nomes das variáveis de entrada e de saída. Os nomes padrão das variáveis de entrada e de saída são **InputDataSet** e **OutputDataSet**, respectivamente. Este script altera os nomes para **SQL_in** e **SQL_out**:

    ```sql
    EXECUTE sp_execute_external_script @language = N'R'
        , @script = N' SQL_out <- SQL_in;'
        , @input_data_1 = N' SELECT 12 as Col;'
        , @input_data_1_name = N'SQL_in'
        , @output_data_1_name = N'SQL_out'
    WITH RESULT SETS(([NewColName] INT NOT NULL));
    ```

    Observe que R diferencia maiúsculas de minúsculas. As variáveis de entrada e saída usadas no script R (**SQL_out**, **SQL_in**) precisam corresponder aos nomes definidos com `@input_data_1_name` e `@output_data_1_name`, incluindo maiúsculas e minúsculas.

   > [!TIP]
   > Só é possível passar um conjunto de dados de entrada como parâmetro, e você pode retornar apenas um conjunto de dados. No entanto, você pode chamar outros conjuntos de dados em seu código R e pode retornar saídas de outros tipos, além do conjunto de dados. Você também pode adicionar a palavra-chave OUTPUT a qualquer parâmetro para que ele retorne com os resultados.

1. Você também pode gerar valores usando apenas o script R sem dados de entrada (`@input_data_1` está definido como em branco).

   O script a seguir gera o texto "Olá" e "mundo".

    ```sql
    EXECUTE sp_execute_external_script @language = N'R'
        , @script = N'
    mytextvariable <- c("hello", " ", "world");
    OutputDataSet <- as.data.frame(mytextvariable);
    '
        , @input_data_1 = N''
    WITH RESULT SETS(([Col1] CHAR(20) NOT NULL));
    ```

    **Resultados**

    ![Resultados da consulta usando @script como entrada](./media/r-data-generated-output.png)

## <a name="check-r-version"></a>Verificar a versão do R

Se você quiser ver qual versão de R está instalada, execute o script a seguir.

```sql
EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'print(version)';
GO
```

A função `print` do R retorna a versão para a janela **Mensagens**. Na saída de exemplo abaixo, você pode ver que, nesse caso, a versão 3.4.4 do R está instalada.

**Resultados**

```text
STDOUT message(s) from external script:
                   _
platform       x86_64-w64-mingw32
arch           x86_64
os             mingw32
system         x86_64, mingw32
status
major          3
minor          4.4
year           2018
month          03
day            15
svn rev        74408
language       R
version.string R version 3.4.4 (2018-03-15)
nickname       Someone to Lean On
```

## <a name="list-r-packages"></a>Listar pacotes do R
::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
A Microsoft fornece vários pacotes do R pré-instalados com os Serviços de Machine Learning.
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
A Microsoft fornece vários pacotes do R pré-instalados com o R Services.
::: moniker-end

Para ver uma lista de quais pacotes do R estão instalados, incluindo informações de versão, dependências, licença e caminho de biblioteca, execute o script a seguir.

```SQL
EXEC sp_execute_external_script @language = N'R'
    , @script = N'
OutputDataSet <- data.frame(installed.packages()[,c("Package", "Version", "Depends", "License", "LibPath")]);'
WITH result sets((
            Package NVARCHAR(255)
            , Version NVARCHAR(100)
            , Depends NVARCHAR(4000)
            , License NVARCHAR(1000)
            , LibPath NVARCHAR(2000)
            ));
```

A saída é de `installed.packages()` em R e é retornada como um conjunto de resultados.

**Resultados**

![Pacotes instalados no R](./media/rsql-installed-packages.png) 

## <a name="next-steps"></a>Próximas etapas

Para saber como usar estruturas de dados ao usar o R com o aprendizado de máquina do SQL, siga este início rápido:

> [!div class="nextstepaction"]
> [Manipular tipos de dados e objetos usando o R com o aprendizado de máquina do SQL](quickstart-r-data-types-and-objects.md)
