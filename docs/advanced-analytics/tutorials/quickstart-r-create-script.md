---
title: 'Início Rápido: Executar scripts de R'
description: Execute um conjunto de scripts R simples com os Serviços de Machine Learning do SQL Server. Saiba como usar o procedimento armazenado sp_execute_external_script para executar o script em uma instância do SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/27/2020
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 495bb56cf76391c8baa1734665d5064b586d4be8
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "76831787"
---
# <a name="quickstart-run-simple-r-scripts-with-sql-server-machine-learning-services"></a>Início Rápido: executar scripts R simples com os Serviços de Machine Learning do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Neste início rápido, você executará um conjunto de scripts R simples usando os [Serviços de Machine Learning do SQL Server](../what-is-sql-server-machine-learning.md). Você aprenderá a usar o procedimento armazenado [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) para executar o script em uma instância do SQL Server.

## <a name="prerequisites"></a>Pré-requisitos

- Este início rápido requer acesso a uma instância do SQL Server que tenha os [Serviços de Machine Learning do SQL Server](../install/sql-machine-learning-services-windows-install.md) com a linguagem R instalada.

  A instância do SQL Server pode ser local ou em uma máquina virtual do Azure. Esteja ciente de que o recurso de script externo está desabilitado por padrão, portanto, talvez seja necessário [habilitar o script externo](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature) e verificar se o **serviço SQL Server Launchpad** está em execução antes de você começar.

- Você também precisa de uma ferramenta para executar consultas SQL que contenham scripts R. Você pode executar esses scripts usando qualquer ferramenta de consulta ou de gerenciamento de banco de dados, desde que ele possa se conectar a uma instância do SQL Server e executar uma consulta T-SQL ou um procedimento armazenado. Esse início rápido usa o [SSMS (SQL Server Management Studio)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms).

## <a name="run-a-simple-script"></a>Executar um script simples

Para executar um script R, você o passará como um argumento para o procedimento armazenado do sistema, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).
Esse procedimento armazenado do sistema inicia o runtime de R no contexto do SQL Server, transmite dados para R, gerencia as sessões de usuário de R com segurança e retorna todos os resultados para o cliente.

Nas etapas a seguir, você executará este script R de exemplo em sua instância do SQL Server:

```r
a <- 1
b <- 2
c <- a/b
d <- a*b
print(c(c, d))
```

1. Abra o **SQL Server Management Studio** e conecte-se à sua instância do SQL Server.

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

| | |
|-|-|
| @language | define a extensão da linguagem a ser chamada, neste caso, R |
| @script | define os comandos passados para o runtime do R. O seu script R inteiro deve ser colocado neste argumento como texto Unicode. Você também pode adicionar texto a uma variável do tipo **nvarchar** e chamar a variável |
| @input_data_1 | dados retornados pela consulta, passados para o runtime R, que retorna os dados ao SQL Server como uma estrutura de dados |
|WITH RESULT SETS | cláusula que define o esquema da tabela de dados retornada para o SQL Server, adicionando "Olá, Mundo" com o nome da coluna, **int** para o tipo de dados |

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

Se você quiser ver qual versão do R está instalada em sua instância do SQL Server, execute o script a seguir.

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

A Microsoft fornece vários pacotes do R pré-instalados com os Serviços de Machine Learning do SQL Server.

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

Para saber como usar estruturas de dados ao usar o R nos Serviços de Machine Learning do SQL Server, siga este guia de início rápido:

> [!div class="nextstepaction"]
> [Manipular tipos de dados e objetos usando o R nos Serviços de Machine Learning do SQL Server](quickstart-r-data-types-and-objects.md)

Para obter mais informações sobre como usar o R nos Serviços de Machine Learning do SQL Server, confira os seguintes artigos:

- [Escrever funções avançadas do R com os Serviços de Machine Learning do SQL Server](quickstart-r-functions.md)
- [Criar e pontuar um modelo de previsão no R com os Serviços de Machine Learning do SQL Server](quickstart-r-train-score-model.md)
- [O que são os Serviços de Machine Learning do SQL Server (Python e R)?](../what-is-sql-server-machine-learning.md)
