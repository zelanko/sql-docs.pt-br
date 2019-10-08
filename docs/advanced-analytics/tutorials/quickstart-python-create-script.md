---
title: Criar e executar scripts Python simples
titleSuffix: SQL Server Machine Learning Services
description: Crie e execute scripts Python simples em uma instância de SQL Server com SQL Server Serviços de Machine Learning.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/04/2019
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: ecf99f1ae70cf44b32955ae164dbe3017bdf5f24
ms.sourcegitcommit: 454270de64347db917ebe41c081128bd17194d73
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/07/2019
ms.locfileid: "72006121"
---
# <a name="quickstart-create-and-run-simple-python-scripts-with-sql-server-machine-learning-services"></a>Início Rápido: Criar e executar scripts Python simples com SQL Server Serviços de Machine Learning
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Neste guia de início rápido, você criará e executará um conjunto de scripts Python simples usando [SQL Server serviços de Machine Learning](../what-is-sql-server-machine-learning.md). Você aprenderá a encapsular um script Python bem formado no procedimento armazenado [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) e executará o script em uma instância de SQL Server.

## <a name="prerequisites"></a>Pré-requisitos

- Este início rápido requer acesso a uma instância do SQL Server com [SQL Server serviços de Machine Learning](../install/sql-machine-learning-services-windows-install.md) com a linguagem Python instalada.

- Você também precisa de uma ferramenta para executar consultas SQL que contêm scripts Python. Você pode executar esses scripts usando qualquer ferramenta de consulta ou gerenciamento de banco de dados, desde que ele possa se conectar a uma instância de SQL Server e executar uma consulta T-SQL ou um procedimento armazenado. Este início rápido usa o [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms).

## <a name="run-a-simple-script"></a>Executar um script simples

Para executar um script Python, você o passará como um argumento para o procedimento armazenado do sistema, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).
Esse procedimento armazenado do sistema inicia o tempo de execução do Python no contexto de SQL Server, passa dados para o Python, gerencia sessões de usuário do Python com segurança e retorna todos os resultados para o cliente.

Nas etapas a seguir, você executará este script Python de exemplo em sua instância de SQL Server:

```python
a = 1
b = 2
c = a/b
d = a*b
print(c, d)
```

1. Abra uma nova janela de consulta no **SQL Server Management Studio** conectado à sua instância do SQL Server.

1. Passe o script Python completo para o procedimento armazenado `sp_execute_external_script`.

   O script é passado pelo argumento `@script`. Tudo dentro do argumento `@script` deve ser um código Python válido.

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

1. O resultado correto é calculado e a função Python `print` retorna o resultado para a janela **mensagens** .

   Ele deve ser semelhante a este.

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

| | |
|-|-|
| @language | define a extensão de linguagem a ser chamada, neste caso, Python |
| @script | define os comandos passados para o tempo de execução do Python<br>Todo o script do Python deve estar incluído nesse argumento, como texto Unicode. Você também pode adicionar o texto a uma variável do tipo **nvarchar** e, em seguida, chamar a variável |
| @input_data_1 | dados retornados pela consulta, passados para o tempo de execução do Python, que retorna os dados para SQL Server como um quadro de dados |
|WITH RESULT SETS | a cláusula define o esquema da tabela de dados retornada para SQL Server, nesse caso, adicionando "Olá, Mundo" como o nome da coluna e **int** para o tipo de dados |

O comando gera o seguinte texto:

| Olá, mundo |
|-------------|
| 1 |

## <a name="use-inputs-and-outputs"></a>Usar entradas e saídas

Por padrão, o `sp_execute_external_script` aceita um único conjunto de dados como entrada, que normalmente você fornece na forma de uma consulta SQL válida. Em seguida, ele retorna um único quadro de dados do Python como saída.

Por enquanto, vamos usar as variáveis de entrada e saída padrão de `sp_execute_external_script`: **InputDataSet** e **OutputDataSet**.

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

1. Execute o script Python a seguir. Ele recupera os dados da tabela usando a instrução `SELECT`, passa-os pelo tempo de execução do Python e retorna os dados como um quadro de dados. A cláusula `WITH RESULT SETS` define o esquema da tabela de dados retornada para SQL, adicionando o nome de coluna *NewColName*.

    ```sql
    EXECUTE sp_execute_external_script @language = N'Python'
        , @script = N'OutputDataSet = InputDataSet;'
        , @input_data_1 = N'SELECT * FROM PythonTestData;'
    WITH RESULT SETS(([NewColName] INT NOT NULL));
    ```

    **Resultados**

    ![Saída do script Python que retorna dados de uma tabela](./media/python-output-pythontestdata.png)

1. Agora, altere os nomes das variáveis de entrada e saída. Os nomes de variáveis de entrada e saída padrão são **InputDataSet** e **OutputDataSet**, o script a seguir altera os nomes para **SQL_in** e **SQL_out**:

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
   > Apenas um conjunto de dados de entrada pode ser passado como um parâmetro e é possível retornar apenas um conjunto de dados. No entanto, você pode chamar outros conjuntos de resultados de dentro de seu código Python e pode retornar saídas de outros tipos além do conjunto de um. Você também pode adicionar a palavra-chave OUTPUT a qualquer parâmetro para que ele seja retornado com os resultados.

1. Você também pode gerar valores usando o script Python sem dados de entrada (`@input_data_1` é definido como em branco).

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
> O Python usa espaços à esquerda para agrupar instruções. Assim, quando o script do Python incorporado abranger várias linhas, como no script anterior, não tente recuar os comandos do Python para que estejam em linha com os comandos SQL. Por exemplo, esse script produzirá um erro:

  ```text
  EXECUTE sp_execute_external_script @language = N'Python'
      , @script = N'
      import pandas as pd
      mytextvariable = pandas.Series(["hello", " ", "world"]);
      OutputDataSet = pd.DataFrame(mytextvariable);
      '
      , @input_data_1 = N''
  WITH RESULT SETS(([Col1] CHAR(20) NOT NULL));
  ```

## <a name="check-python-version"></a>Verificar a versão do Python

Se você quiser ver qual versão do Python está instalada em sua instância de SQL Server, execute o script a seguir.

```sql
EXECUTE sp_execute_external_script @language = N'Python'
    , @script = N'
import sys
print(sys.version)
'
GO
```

A função Python `print` retorna a versão para a janela **mensagens** . Na saída de exemplo abaixo, você pode ver que, nesse caso, o Python versão 3.5.2 está instalado.

**Resultados**

```text
STDOUT message(s) from external script: 
3.5.2 |Continuum Analytics, Inc.| (default, Jul  5 2016, 11:41:13) [MSC v.1900 64 bit (AMD64)]
```

## <a name="list-python-packages"></a>Listar pacotes python

A Microsoft fornece vários pacotes do Python pré-instalados com SQL Server Serviços de Machine Learning em sua instância do SQL Server.

Para ver uma lista de quais pacotes do Python estão instalados, incluindo a versão, execute o script a seguir.

```SQL
EXECUTE sp_execute_external_script @language = N'Python'
    , @script = N'
import pip
for i in pip.get_installed_distributions():
    print(i)
'
GO
```

A saída é de `pip.get_installed_distributions()` no Python e retornada como mensagens `STDOUT`.

**Resultados**

```text
STDOUT message(s) from external script:
xlwt 1.2.0
XlsxWriter 0.9.6
xlrd 1.0.0
win-unicode-console 0.5
widgetsnbextension 2.0.0
wheel 0.29.0
Werkzeug 0.12.1
wcwidth 0.1.7
unicodecsv 0.14.1
traitlets 4.3.2
tornado 4.4.2
toolz 0.8.2
. . .
```

## <a name="next-steps"></a>Próximas etapas

Para saber como usar estruturas de dados ao usar o Python no SQL Server Serviços de Machine Learning, siga este guia de início rápido:

> [!div class="nextstepaction"]
> [Manipular tipos de dados e objetos usando Python no SQL Server Serviços de Machine Learning](quickstart-python-data-structures.md)

Para obter mais informações sobre como usar o Python no SQL Server Serviços de Machine Learning, consulte os seguintes artigos:

- [Escrever funções avançadas do Python com o SQL Server Serviços de Machine Learning](quickstart-python-functions.md)
- [Criar e pontuar um modelo de previsão em Python com SQL Server Serviços de Machine Learning](quickstart-python-train-score-model.md)
- [O que é SQL Server Serviços de Machine Learning (Python e R)?](../what-is-sql-server-machine-learning.md)
