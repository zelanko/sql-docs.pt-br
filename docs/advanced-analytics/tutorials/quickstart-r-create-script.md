---
title: Criar e executar scripts R simples
titleSuffix: SQL Server Machine Learning Services
description: Crie e execute scripts R simples em uma instância de SQL Server com SQL Server Serviços de Machine Learning.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/17/2019
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: d723fa9b90659eb31e96626a3a85c1299c17fa2f
ms.sourcegitcommit: 1661c3e1bb38ed12f8485c3860fc2d2b97dd2c9d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/20/2019
ms.locfileid: "71150309"
---
# <a name="quickstart-create-and-run-simple-r-scripts-with-sql-server-machine-learning-services"></a>Início Rápido: Criar e executar scripts R simples com SQL Server Serviços de Machine Learning
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Neste guia de início rápido, você criará e executará um conjunto de scripts R simples usando [SQL Server serviços de Machine Learning](../what-is-sql-server-machine-learning.md). Você aprenderá a encapsular um script R bem formado no procedimento armazenado [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) e executará o script em uma instância de SQL Server.

## <a name="prerequisites"></a>Pré-requisitos

- Este início rápido requer acesso a uma instância do SQL Server com [SQL Server serviços de Machine Learning](../install/sql-machine-learning-services-windows-install.md) com a linguagem R instalada.

  Sua instância de SQL Server pode estar em uma máquina virtual do Azure ou no local. Apenas esteja ciente de que o recurso de script externo está desabilitado por padrão, portanto, talvez seja necessário [habilitar o script externo](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature) e verificar se **SQL Server Launchpad serviço** está em execução antes de iniciar.

- Você também precisa de uma ferramenta para executar consultas SQL que contenham scripts R. Você pode executar esses scripts usando qualquer ferramenta de consulta ou gerenciamento de banco de dados, desde que ele possa se conectar a uma instância de SQL Server e executar uma consulta T-SQL ou um procedimento armazenado. Este início rápido usa o [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms).

## <a name="run-a-simple-script"></a>Executar um script simples

Para executar um script R, você o passará como um argumento para o procedimento armazenado do sistema, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).
Esse procedimento armazenado do sistema inicia o tempo de execução do R no contexto de SQL Server, passa dados para o R, gerencia as sessões de usuário do R com segurança e retorna todos os resultados para o cliente.

Nas etapas a seguir, você executará este script R de exemplo em sua instância de SQL Server:

```r
a <- 1
b <- 2
c <- a/b
d <- a*b
print(c(c, d))
```

1. Abra **SQL Server Management Studio** e conecte-se à sua instância do SQL Server.

1. Passe o script R completo para o `sp_execute_external_script` procedimento armazenado.

   O script é passado pelo `@script` argumento. Tudo dentro do `@script` argumento deve ser um código R válido.

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

1. O resultado correto é calculado e a função `print` R retorna o resultado para a janela **mensagens** .

   Ele deve ser semelhante a este.

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

As entradas para `sp_execute_external_script` o procedimento armazenado incluem:

| | |
|-|-|
| @language | define a extensão de linguagem para chamar, neste caso, R |
| @script | define os comandos passados para o tempo de execução de R. Todo o script R deve ser colocado neste argumento, como texto Unicode. Você também pode adicionar o texto a uma variável do tipo **nvarchar** e, em seguida, chamar a variável |
| @input_data_1 | dados retornados pela consulta, passados para o tempo de execução de R, que retorna os dados para SQL Server como um quadro de dados |
|COM CONJUNTOS DE RESULTADOS | a cláusula define o esquema da tabela de dados retornada para SQL Server, adicionando "Olá, Mundo" como o nome da coluna, **int** para o tipo de dados |

O comando gera o seguinte texto:

| Olá, mundo |
|-------------|
| 1 |

## <a name="use-inputs-and-outputs"></a>Usar entradas e saídas

Por padrão, `sp_execute_external_script` o aceita um único conjunto de dados como entrada, que normalmente você fornece na forma de uma consulta SQL válida. Em seguida, ele retorna um único quadro de dados do R como saída.

Por enquanto, vamos usar as variáveis de entrada e saída padrão de `sp_execute_external_script`: **InputDataSet** e **OutputDataSet**.

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

1. Use a `SELECT` instrução para consultar a tabela.
  
    ```sql
    SELECT *
    FROM RTestData
    ```

    **Resultados**

    ![Conteúdo da tabela RTestData](./media/select-rtestdata.png)

1. Execute o script R a seguir. Ele recupera os dados da tabela usando a `SELECT` instrução, passa-os pelo tempo de execução do R e retorna os dados como um quadro de dados. A `WITH RESULT SETS` cláusula define o esquema da tabela de dados retornada para SQL, adicionando o nome de coluna *NewColName*.

    ```sql
    EXECUTE sp_execute_external_script @language = N'R'
        , @script = N'OutputDataSet <- InputDataSet;'
        , @input_data_1 = N'SELECT * FROM RTestData;'
    WITH RESULT SETS(([NewColName] INT NOT NULL));
    ```

    **Resultados**

    ![Saída do script R que retorna dados de uma tabela](./media/r-output-rtestdata.png)

1. Agora, vamos alterar os nomes das variáveis de entrada e saída. Os nomes de variáveis de entrada e saída padrão são **InputDataSet** e **OutputDataSet**, esse script altera os nomes para **SQL_in** e **SQL_out**:

    ```sql
    EXECUTE sp_execute_external_script @language = N'R'
        , @script = N' SQL_out <- SQL_in;'
        , @input_data_1 = N' SELECT 12 as Col;'
        , @input_data_1_name = N'SQL_in'
        , @output_data_1_name = N'SQL_out'
    WITH RESULT SETS(([NewColName] INT NOT NULL));
    ```

    Observe que o R diferencia maiúsculas de minúsculas. As variáveis de entrada e saída usadas no script R (**SQL_out**, **SQL_in**) precisam corresponder aos nomes definidos com `@input_data_1_name` and, incluindo maiúsculas e `@output_data_1_name`minúsculas.

   > [!TIP]
   > Apenas um conjunto de dados de entrada pode ser passado como um parâmetro e é possível retornar apenas um conjunto de dados. No entanto, você pode chamar outros conjuntos de dados no código do R e retornar saídas de outros tipos, além do conjunto de dados. Você também pode adicionar a palavra-chave OUTPUT a qualquer parâmetro para que ele seja retornado com os resultados.

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

    ![Resultados da consulta @script usando como entrada](./media/r-data-generated-output.png)

## <a name="check-r-version"></a>Verificar a versão do R

Se você quiser ver qual versão do R está instalada em sua instância do SQL Server, execute o script a seguir.

```sql
EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'print(version)';
GO
```

A função `print` R retorna a versão para a janela **mensagens** . Na saída de exemplo abaixo, você pode ver que, nesse caso, o R versão 3.4.4 está instalado.

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

## <a name="list-r-packages"></a>Listar pacotes de R

A Microsoft fornece vários pacotes de R pré-instalados com SQL Server Serviços de Machine Learning.

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

A saída é de `installed.packages()` em R e retornada como um conjunto de resultados.

**Resultados**

![Pacotes instalados em R](./media/rsql-installed-packages.png) 

## <a name="next-steps"></a>Próximas etapas

Para criar um modelo de aprendizado de máquina usando R no SQL Server, siga este guia de início rápido:

> [!div class="nextstepaction"]
> [Criar e pontuar um modelo de previsão em R com SQL Server Serviços de Machine Learning](quickstart-r-train-score-model.md)

Para obter mais informações sobre SQL Server Serviços de Machine Learning, consulte os artigos a seguir.

- [Manipular tipos de dados e objetos usando R no SQL Server Serviços de Machine Learning](quickstart-r-data-types-and-objects.md)
- [Escrever funções de R avançadas com SQL Server Serviços de Machine Learning](quickstart-r-functions.md)
- [O que é SQL Server Serviços de Machine Learning (Python e R)?](../what-is-sql-server-machine-learning.md)
