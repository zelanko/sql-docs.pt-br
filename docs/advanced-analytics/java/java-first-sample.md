---
title: Exemplo de Java e um tutorial para SQL Server 2019 - serviços do SQL Server Machine Learning
description: Execute o código de exemplo do Java no SQL Server de 2019 para saber as etapas para usar a extensão da linguagem Java com dados do SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/23/2019
ms.topic: conceptual
author: nelgson
ms.author: negust
ms.reviewer: dphansen
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 000318716b07f58e94bd5c482d9c349e5d4e5481
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63473770"
---
# <a name="sql-server-regex-java-sample"></a>SQL Server Regex Java Sample

Este exemplo demonstra uma classe Java que recebe duas colunas (ID e texto) do SQL Server e também usa uma expressão regular como um parâmetro de entrada. A classe retorna duas colunas de volta para o SQL Server (ID e texto).

Para um determinado texto na coluna de texto enviada para a classe de Java, o código verifica se a expressão regular especificada é atendida e retorna esse texto junto com a ID original. 

Esse exemplo específico usa uma expressão regular que verifica se um texto contiver a palavra "Java" ou "java".

## <a name="microsoft-extensibility-sdk-for-java-for-microsoft-sql-server"></a>Extensibilidade do Microsoft SDK para Java para o Microsoft SQL Server

 No CTP 2.5, estamos alterando a maneira como você implementa o código Java que usa a extensão da linguagem Java para se comunicar com o SQL Server. Isso fornecerá uma melhor experiência de desenvolvedor ao interagir com o SQL Server a partir de Java.

Você deve pensar sobre o SDK como uma interface do auxiliar, o que torna mais fácil de implementar o código Java em execução no SQL Server.

> [!NOTE]
> A introdução do SDK é uma grande mudança de CTPs anteriores. Todos os exemplos anteriores tinham o trabalho precisará ser atualizado para usar o SDK.

Para obter mais informações, consulte o [documentação do SDK](java-sdk.md).

## <a name="prerequisites"></a>Prerequisites

+ Instância do mecanismo de banco de dados do SQL Server de 2019 com a estrutura de extensibilidade e a extensão de programação Java [no Windows](../install/sql-machine-learning-services-windows-install.md) ou [no Linux](https://docs.microsoft.com/sql/linux/sql-server-linux-setup). Para obter mais informações sobre a configuração do sistema, consulte [extensão da linguagem Java no SQL Server 2019](extension-java.md). Para obter mais informações sobre requisitos de codificação, consulte [como chamar o Java no SQL Server](howto-call-java-from-sql.md).

+ SQL Server Management Studio ou no Studio de dados do Azure para a execução de T-SQL.

+ Java SE Development Kit (JDK) 8 ou o JRE 8 Windows nos ou no Linux.

+ [SDK de extensibilidade do Microsoft Java para o Microsoft SQL Server](http://aka.ms/mssql-java-lang-extension) mssql-java-lang-extension.jar.

Compilação de linha de comando usando **javac** é suficiente para este tutorial.

## <a name="1---create-sample-data-in-a-sql-server-table"></a>1 - criar dados de exemplo em uma tabela do SQL Server

Primeiro, criar e preencher uma *testdata* de tabela com **ID** e **texto** colunas. Conectar-se ao SQL Server e execute o script a seguir para criar uma tabela:

```sql
CREATE DATABASE javatest
GO
USE javatest
GO

-- Create table for test data
DROP TABLE IF exists testdata;
GO

CREATE TABLE testdata(
id int NOT NULL,
"text" nvarchar(100) NOT NULL)
GO

TRUNCATE TABLE testdata
GO

-- Insert data into test table
INSERT INTO testdata(id, "text") VALUES (1, 'This sentence contains java')
INSERT INTO testdata(id, "text") VALUES (2, 'This sentence does not')
INSERT INTO testdata(id, "text") VALUES (3, 'I love Java!')
GO
Select * FROM testdata
```

## <a name="2---class-regexsamplejava"></a>2 - classe RegexSample.java

Comece criando a classe principal.

Nesta etapa, crie uma classe chamada **RegexSample.java** e copie o seguinte código Java para esse arquivo.

Essa classe principal está importando o SDK, que significa que o arquivo jar baixado na etapa 1 precisa ser detectável dessa classe.

> [!NOTE]
> Observe que essa classe importa o pacote do SDK de extensão Java.
Consulte o artigo o [extensibilidade de Microsoft SDK para Java para o Microsoft SQL Server](java-sdk.md) para obter mais detalhes.

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

## <a name="3-compile-and-create-jar-file"></a>3 compilar e criar o arquivo. jar

É recomendável que você empacotar suas classes e as dependências em arquivos. jar. A maioria dos IDEs do Java, como Eclipse ou IntelliJ suporte gerar arquivos jar quando você compilação/Compilar o projeto. Neste exemplo, que nomeamos o arquivo jar **regex.jar**.

Se você estiver manualmente criando um arquivo. jar, você pode seguir as etapas, consulte [como criar um arquivo jar](extension-java.md#create-jar).

> [!NOTE]
> Esse exemplo usa pacotes, o que significa que o pacote "pkg" fornecido na parte superior da classe torna-se de que o código compilado é salvo em uma subpasta chamada "pkg". Isso é feita automaticamente se você usar um IDE, mas se você estiver compilando manualmente classes usando **javac**, você precisará colocar o código compilado na pasta pkg sub manualmente.

## <a name="4---create-external-libraries"></a>4 - criar bibliotecas externas

Criando uma biblioteca externa, do SQL Server terão automaticamente acesso para os arquivos jar e você não precisará definir permissões especiais ao classpath.

Neste exemplo, você precisará criar duas bibliotecas externas. Um para o SDK e outro para o exemplo de Java de Regex.

1.  Baixe [extensibilidade de Microsoft SDK para Java para o Microsoft SQL Server](http://aka.ms/mssql-java-lang-extension) mssql-java-lang-extension.jar.

1. Criar uma biblioteca externa para o sdk

```sql
-- Create external library for the SDK
CREATE EXTERNAL LIBRARY sdk
FROM (CONTENT = '<path>/mssql-java-lang-extension.jar')
WITH (LANGUAGE = 'Java');
GO
```

3. Criar uma biblioteca externa para o exemplo de regex

```sql
-- Create external library for the regex sample
CREATE EXTERNAL LIBRARY regex
FROM (CONTENT = '<path>/regex.jar')
WITH (LANGUAGE = 'Java');
GO
```

## <a name="5---set-permissions-skip-if-you-performed-step-4"></a>5 – definir permissões (Ignorar se você tiver executado a etapa 4)

Essa etapa não é necessária se você usar bibliotecas externas. A maneira recomendada de trabalho é criar uma biblioteca externa do jar de você.

Se você não quiser usar bibliotecas externas, você precisará definir as permissões necessárias. Execução do script é bem-sucedido somente se as identidades de processo tem acesso ao seu código. Você pode encontrar mais informações sobre como definir permissões [aqui](extension-java.md).

### <a name="on-linux"></a>On Linux

Conceder permissões de leitura/execução no classpath para o **mssql_satellite** usuário.

### <a name="on-windows"></a>No Windows

Conceda as permissões 'Leitura e Execute' **SQLRUserGroup** e o **todos os pacotes de aplicativos** SID na pasta que contém o código Java compilado. 

Toda a árvore deve ter as permissões, da raiz pai para a última pasta sub. 
 
1. Clique com botão direito na pasta (por exemplo, ' C:\myJavaCode'), escolha **propriedades** > **segurança**.
2. Clique em **Editar**.
3. Clique em **Adicionar**.
4. Na **selecionar usuários, computador, contas de serviço ou grupos**:
   + Clique em **tipos de objetos** e verifique se *princípios de segurança internas* e *grupos* estão selecionados.
   + Clique em **locais** para selecionar o nome do computador local na parte superior da lista.
5. Insira **SQLRUserGroup**, verifique o nome e, em seguida, clique em Okey para adicionar o grupo.
6. Insira **todos os pacotes de aplicativos**, verifique o nome e, em seguida, clique em Okey para adicionar. Se o nome não for resolvido, reveja a etapa de locais. O SID é local para seu computador.

Verifique se que ambas as identidades de segurança tem permissões de 'Leitura e execução' na pasta e subpasta de "pacote".

<a name="call-method"></a>

## <a name="2---call-the-java-class"></a>2 - chamar a classe de Java

Para chamar o código Java a partir do SQL Server, vamos criar um procedimento armazenado que chama sp_execute_external_script. O parâmetro "script", definiremos qual [pacote]. [class] que desejamos chamar. Neste exemplo, a classe pertence a um pacote chamado **pkg** e um arquivo de classe chamado **RegexSample.java**.

> [!NOTE]
>Não definimos qual método chamar. Por padrão, o **executar** método será chamado. Isso significa que você precisa seguir a interface do SDK e implementar um método execute na sua classe de Java, se você quiser ser capaz de chamar a classe do SQL Server.

```sql
/*
This stored procedure takes an input query (input dataset) and a regular expression and returns the rows that fulfilled the given regular expression. This sample uses a regular expression that checks if a text contains the word "Java" or "java" ([Jj]ava) 
*/

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

Depois de executar a chamada, você deve obter um conjunto de resultados com duas da linhas.

![Os resultados do exemplo de Java](../media/java/java-sample-results.png "resultados de exemplo")

### <a name="if-you-get-an-error"></a>Se você receber um erro

+ Quando você compila suas classes, a subpasta "pkg" deve conter o código compilado para todas as três classes.

+ Por fim, se você não estiver usando bibliotecas externas, verificar permissões no *cada* pasta da raiz até a subpasta "pkg", para garantir que as identidades de segurança que executa o processo externo tenham permissão para ler e executar seu código.

## <a name="next-steps"></a>Próximas etapas

+ [Extensibilidade do Microsoft SDK para Java para o Microsoft SQL Server](java-sdk.md)
+ [Como chamar o Java no SQL Server](howto-call-java-from-sql.md)
+ [Extensões de Java no SQL Server](extension-java.md)
+ [Tipos de dados Java e o SQL Server](java-sql-datatypes.md)
