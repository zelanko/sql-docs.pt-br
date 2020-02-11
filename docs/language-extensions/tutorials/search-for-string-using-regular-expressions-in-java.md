---
title: 'Tutorial: Pesquisa de cadeia de caracteres Regex em Java'
description: Este tutorial mostra como usar Extensões de Linguagem do SQL Server e executar código Java que pesquisa uma cadeia de caracteres com expressões regulares (regex).
author: dphansen
ms.author: davidph
ms.date: 11/05/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 9740e8c93fbac0d7727ba9922342df96d9190e10
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "73658798"
---
# <a name="tutorial-search-for-a-string-using-regular-expressions-regex-in-java"></a>Tutorial: Pesquisar uma cadeia de caracteres usando regex (expressões regulares) em Java
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este tutorial mostra como usar [Extensões de Linguagem do SQL Server](../language-extensions-overview.md) e criar uma classe Java que recebe duas colunas (ID e texto) do SQL Server e uma expressão regular (regex) como um parâmetro de entrada. A classe retorna duas colunas de volta para SQL Server (ID e texto).

Para um determinado texto na coluna de texto enviado para a classe Java, o código verifica se determinada expressão regular é atendida e retorna esse texto com a ID original.

Este código de exemplo usa uma expressão regular que verifica se um texto contém a palavra "Java" ou "java".

## <a name="prerequisites"></a>Prerequisites

+ Instância do Mecanismo de Banco de Dados do SQL Server 2019 com a estrutura de extensibilidade e a extensão de programação do Java [no Windows](../install/install-sql-server-language-extensions-on-windows.md) ou [no Linux](https://docs.microsoft.com/sql/linux/sql-server-linux-setup-language-extensions). Para obter mais informações, confira [Extensão de Linguagem no SQL Server 2019](../language-extensions-overview.md). Para obter mais informações sobre requisitos de codificação, confira [Como chamar o Java no SQL Server](../how-to/call-java-from-sql.md).

+ SQL Server Management Studio ou Azure Data Studio para executar T-SQL.

+ JDK (Java SE Development Kit) 8 ou JRE 8 no Windows ou Linux.

+ O arquivo **mssql-java-lang-extension.jar** do [SDK de Extensibilidade da Microsoft para Java para o Microsoft SQL Server](../how-to/extensibility-sdk-java-sql-server.md) .

A compilação da linha de comando usando **javac** é suficiente para este tutorial.

## <a name="create-sample-data"></a>Criar dados de exemplo

Primeiro, crie um banco de dados e popule uma tabela **testdata** com as colunas **ID** e **texto**.

```sql
CREATE DATABASE javatest
GO

USE javatest
GO

CREATE TABLE testdata (
    id int NOT NULL,
    "text" nvarchar(100) NOT NULL
)
GO

-- Insert data into test table
INSERT INTO testdata(id, "text") VALUES (1, 'This sentence contains java')
INSERT INTO testdata(id, "text") VALUES (2, 'This sentence does not')
INSERT INTO testdata(id, "text") VALUES (3, 'I love Java!')
GO
```

## <a name="create-the-main-class"></a>Criar a classe principal

Nesta etapa, crie um arquivo de classe chamado **RegexSample.java** e copie o seguinte código Java para esse arquivo.

Essa classe principal importará o SDK, o que significa que o arquivo jar baixado na etapa 1 precisa ser detectável nessa classe.

```java
package pkg;

import com.microsoft.sqlserver.javalangextension.PrimitiveDataset;
import com.microsoft.sqlserver.javalangextension.AbstractSqlServerExtensionExecutor;
import java.util.LinkedHashMap;
import java.util.LinkedList;
import java.util.ListIterator;
import java.util.regex.*;

public class RegexSample extends AbstractSqlServerExtensionExecutor {
    private Pattern expr;

    public RegexSample() {
        // Setup the expected extension version, and class to use for input and output dataset
        executorExtensionVersion = SQLSERVER_JAVA_LANG_EXTENSION_V1;
        executorInputDatasetClassName = PrimitiveDataset.class.getName();
        executorOutputDatasetClassName = PrimitiveDataset.class.getName();
    }
    
    public PrimitiveDataset execute(PrimitiveDataset input, LinkedHashMap<String, Object> params) {
        // Validate the input parameters and input column schema
        validateInput(input, params);

        int[] inIds = input.getIntColumn(0);
        String[] inValues = input.getStringColumn(1);
        int rowCount = inValues.length;

        String regexExpr = (String)params.get("regexExpr");
        expr = Pattern.compile(regexExpr);

        System.out.println("regex expression: " + regexExpr);

        // Lists to store the output data
        LinkedList<Integer> outIds = new LinkedList<Integer>();
        LinkedList<String> outValues = new LinkedList<String>();

        // Evaluate each row
        for(int i = 0; i < rowCount; i++) {
            if (check(inValues[i])) {
                outIds.add(inIds[i]);
                outValues.add(inValues[i]);
            }
        }

        int outputRowCount = outValues.size();

        int[] idOutputCol = new int[outputRowCount];
        String[] valueOutputCol = new String[outputRowCount];

        // Convert the list of output columns to arrays
        outValues.toArray(valueOutputCol);

        ListIterator<Integer> it = outIds.listIterator(0);
        int rowId = 0;

        System.out.println("Output data:");
        while (it.hasNext()) {
            idOutputCol[rowId] = it.next().intValue();

            System.out.println("ID: " + idOutputCol[rowId] + " Value: " + valueOutputCol[rowId]);
            rowId++;
        }

        // Construct the output dataset
        PrimitiveDataset output = new PrimitiveDataset();

        output.addColumnMetadata(0, "ID", java.sql.Types.INTEGER, 0, 0);
        output.addColumnMetadata(1, "Text", java.sql.Types.NVARCHAR, 0, 0);

        output.addIntColumn(0, idOutputCol, null);
        output.addStringColumn(1, valueOutputCol);

        return output;
    }

    private void validateInput(PrimitiveDataset input, LinkedHashMap<String, Object> params) {
        // Check for the regex expression input parameter
        if (params.get("regexExpr") == null) {
            throw new IllegalArgumentException("Input parameter 'regexExpr' is not found");
        }

        // The expected input schema should be at least 2 columns, (INTEGER, STRING)
        if (input.getColumnCount() < 2) {
            throw new IllegalArgumentException("Unexpected input schema, schema should be an (INTEGER, NVARCHAR or VARCHAR)");
        }

        // Check that the input column types are expected
        if (input.getColumnType(0) != java.sql.Types.INTEGER &&
                (input.getColumnType(1) != java.sql.Types.VARCHAR && input.getColumnType(1) == java.sql.Types.NVARCHAR )) {
            throw new IllegalArgumentException("Unexpected input schema, schema should be an (INTEGER, NVARCHAR or VARCHAR)");
        }
    }

    private boolean check(String text) {
        Matcher m = expr.matcher(text);

        return m.find();
    }
}
```

## <a name="compile-and-create-a-jar-file"></a>Compilar e criar um arquivo .jar

Empacote suas classes e dependências em um arquivo `.jar`. A maioria dos Java IDEs (por exemplo, Eclipse ou IntelliJ) dá suporte à geração de arquivos `.jar` quando você cria ou compila o projeto. Dê o arquivo `.jar` o nome **regex.jar**.

Se você não estiver usando um Java IDE, poderá criar manualmente um arquivo `.jar`. Para obter mais informações, confira [Como criar um arquivo jar do Java com base em arquivos de classe](../how-to/create-a-java-jar-file-from-class-files.md).

> [!NOTE]
> Este tutorial usa pacotes. A linha `package pkg;` na parte superior da classe verifica se o código compilado foi salvo em uma subpasta chamada **pkg**. Se você usar um IDE, o código compilado será salvo automaticamente nesta pasta. Se você usar o **javac** para compilar manualmente as classes, precisará colocar o código compilado na pasta **pkg**.

## <a name="create-external-language"></a>Criar linguagem externa

Você precisa criar uma linguagem externa no banco de dados. A linguagem externa é um objeto com escopo de banco de dados, o que significa que linguagens externas como Java precisam ser criadas para cada banco de dados no qual você deseja usá-las.

### <a name="create-external-language-on-windows"></a>Criar linguagem externa no Windows

Se você estiver usando o Windows, siga as etapas abaixo para criar uma linguagem externa para Java.

1. Crie um arquivo .zip que contém a extensão.

    Como parte da instalação do SQL Server no Windows, a extensão Java **.zip** é instalada nesta localização: `[SQL Server install path]\MSSQL\Binn\java-lang-extension.zip`. Esse arquivo zip contém a **javaextension.dll**.

2. Crie uma linguagem Java externa com base no arquivo .zip:

    ```sql
    CREATE EXTERNAL LANGUAGE Java
    FROM
    (CONTENT = N'[SQL Server install path]\MSSQL\Binn\java-lang-extension.zip', FILE_NAME = 'javaextension.dll',
    ENVIRONMENT_VARIABLES = N'{"JRE_HOME":"<path to JRE>"}' );
    GO
    ```

### <a name="create-external-language-on-linux"></a>Criar linguagem externa no Linux

Como parte da instalação, o arquivo de extensão **.tar.gz** é salvo no caminho a seguir: `/opt/mssql-extensibility/lib/java-lang-extension.tar.gz`.

Para criar uma linguagem Java externa, execute a seguinte instrução T-SQL no Linux:

```sql
CREATE EXTERNAL LANGUAGE Java
FROM (CONTENT = N'/opt/mssql-extensibility/lib/java-lang-extension.tar.gz', file_name = 'javaextension.so',
ENVIRONMENT_VARIABLES = N'{"JRE_HOME":"<path to JRE>"}' );
GO
```

### <a name="permissions-to-execute-external-language"></a>Permissões para executar a linguagem externa

Para executar o código Java, um usuário precisa receber a execução de script externo nessa linguagem específica.

Para obter mais informações, confira [CREATE EXTERNAL LANGUAGE](https://docs.microsoft.com/sql/t-sql/statements/create-external-language-transact-sql).

## <a name="create-external-libraries"></a>Criar bibliotecas externas

Use [CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) para criar uma biblioteca externa para seus arquivos `.jar`. O SQL Server terá acesso aos arquivos `.jar` e você não precisará definir nenhuma permissão especial para o **classpath**.

Nesse exemplo, você criará duas bibliotecas externas. Uma para o SDK e outra para o código Java RegEx.

1. O arquivo jar do SDK **mssql-java-lang-extension.jar** é instalado como parte do SQL Server 2019 no Windows e no Linux.

    + Caminho de instalação padrão no Windows: **[diretório base de instalação da instância]\MSSQL\Binn\mssql-java-lang-extension.jar**

    + Caminho de instalação padrão no Linux: **/opt/mssql/lib/mssql-java-lang-extension.jar**

    O código também é de software livre e pode ser encontrado no [Repositório GitHub de Extensões de Linguagem do SQL Server](https://github.com/microsoft/sql-server-language-extensions). Para obter informações, confira o [SDK de Extensibilidade da Microsoft para Java para o Microsoft SQL Server](../how-to/extensibility-sdk-java-sql-server.md).

2. Crie uma biblioteca externa para o SDK.

    ```sql
    CREATE EXTERNAL LIBRARY sdk
    FROM (CONTENT = '<OS specific path from above>/mssql-java-lang-extension.jar')
    WITH (LANGUAGE = 'Java');
    GO
    ```

3. Crie uma biblioteca externa para o código RegEx.

    ```sql
    CREATE EXTERNAL LIBRARY regex
    FROM (CONTENT = '<path>/regex.jar')
    WITH (LANGUAGE = 'Java');
    GO
    ```

## <a name="set-permissions"></a>Definir permissões

> [!NOTE]
> Ignore esta etapa se você usar bibliotecas externas na etapa anterior. A maneira recomendada é criar uma biblioteca externa do seu arquivo `.jar`.

Se não desejar usar bibliotecas externas, você precisará definir as permissões necessárias. A execução do script só terá êxito se as identidades do processo tiverem acesso ao seu código. Você pode encontrar mais informações sobre como definir permissões no [guia de instalação](../install/install-sql-server-language-extensions-on-windows.md).

### <a name="on-linux"></a>No Linux

Conceda permissões de leitura/execução no classpath ao usuário **mssql_satellite**.

### <a name="on-windows"></a>No Windows

Conceda permissões de 'Leitura e Execução' à SID de **SQLRUserGroup** e de **Todos os pacotes de aplicativos** na pasta que contém seu código Java compilado.

Toda a árvore deve ter permissões, do pai raiz até a última subpasta.

1. Clique com o botão direito do mouse na pasta (por exemplo, `C:\myJavaCode`) e selecione **Propriedades** > **Segurança**.
2. Clique em **Editar**.
3. Clique em **Adicionar**.
4. Em **Selecionar Usuários, Computador, Contas de Serviço ou Grupos**:
   1. Clique em **Tipos de Objeto** e verifique se *Princípios de segurança interna* e *Grupos* estão selecionados.
   2. Clique em **Locais** para selecionar o nome do computador local na parte superior da lista.
5. Insira **SQLRUserGroup**, verifique o nome e clique em OK para adicionar o grupo.
6. Insira **TODOS OS PACOTES DE APLICATIVOS**, verifique o nome e clique em OK para adicionar. 
    Se o nome não resolver, acesse novamente a etapa Locais. A SID é local em seu computador.

Verifique se as duas identidades de segurança têm as permissões **Leitura e Execução** na pasta e na subpasta **pkg**.

<a name="call-method"></a>

## <a name="call-the-java-class"></a>Chamar a classe Java

Crie um procedimento armazenado que chama `sp_execute_external_script` para chamar o código Java do SQL Server. No parâmetro **script**, defina qual `package.class` você deseja chamar. No código abaixo, a classe pertence a um pacote chamado **pkg** e um arquivo de classe chamado **RegexSample.java**.

> [!NOTE]
> O código não está definindo qual método chamar. Por padrão, o método **execute** será chamado. Isso significa que você precisará seguir a interface do SDK e implementar um método execute em sua classe Java se desejar poder chamar a classe do SQL Server.

O procedimento armazenado usa uma consulta de entrada (conjunto de dados de entrada) e uma expressão regular e retorna as linhas que cumpriram a expressão regular fornecida. Ele usa uma expressão regular `[Jj]ava` que verifica se um texto contém a palavra **Java** ou **java**.

```sql
CREATE OR ALTER PROCEDURE [dbo].[java_regex] @expr nvarchar(200), @query nvarchar(400)
AS
BEGIN
--Call the Java program by giving the package.className in @script
--The method invoked in the Java code is always the "execute" method
EXEC sp_execute_external_script
  @language = N'Java'
, @script = N'pkg.RegexSample'
, @input_data_1 = @query
, @params = N'@regexExpr nvarchar(200)'
, @regexExpr = @expr
with result sets ((ID int, text nvarchar(100)));
END
GO

--Now execute the above stored procedure and provide the regular expression and an input query
EXECUTE [dbo].[java_regex] N'[Jj]ava', N'SELECT id, text FROM testdata'
GO
```

### <a name="results"></a>Resultados

Após executar a chamada, você deve obter um conjunto de resultados com duas das linhas.

![Resultados do exemplo de Java](../media/java/java-sample-results.png "Resultados de exemplo")

### <a name="if-you-get-an-error"></a>Se você receber um erro

+ Quando você compilar suas classes, a subpasta **pkg** deverá conter o código compilado para todas as três classes.

+ Se você não estiver usando bibliotecas externas, verifique as permissões em *cada* pasta, desde a subpasta **raiz** até a **pkg**, para verificar se as identidades de segurança que executam o processo externo têm permissão para ler e executar seu código.

## <a name="next-steps"></a>Próximas etapas

+ [Como chamar Java no SQL Server](../how-to/call-java-from-sql.md)
+ [Extensões do Java no SQL Server](../language-extensions-overview.md)
+ [Tipos de dados Java e SQL Server](../how-to/java-to-sql-data-types.md)
