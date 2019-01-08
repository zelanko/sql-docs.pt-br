---
title: Exemplo de Java e um tutorial para SQL Server 2019 - serviços do SQL Server Machine Learning
description: Execute o código de exemplo do Java no SQL Server de 2019 para saber as etapas para usar a extensão da linguagem Java com dados do SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/24/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 32c0792882020612c40a0c41b1c54aaeb51da91c
ms.sourcegitcommit: 15b780aa5abe3f42cd70b6edf7d5a645e990b618
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/07/2019
ms.locfileid: "54069047"
---
# <a name="sql-server-java-sample-walkthrough"></a>Instruções passo a passo de exemplo do Java do SQL Server

Este exemplo demonstra uma classe Java que recebe duas colunas (ID e texto) do SQL Server e retorna duas colunas de volta para o SQL Server (ID e ngram). Para uma determinada ID e a combinação de cadeia de caracteres, o código gera permutações de ngrams (subcadeias de caracteres), retornando essas permutas sem dificuldades, juntamente com a ID original. O comprimento do ngram é definido por um parâmetro enviado para a classe de Java.

## <a name="prerequisites"></a>Prerequisites

+ Instância do mecanismo de banco de dados do SQL Server de 2019 com a estrutura de extensibilidade e a extensão de programação Java [no Windows](../install/sql-machine-learning-services-windows-install.md) ou [no Linux](https://docs.microsoft.com/sql/linux/sql-server-linux-setup). Para obter mais informações sobre a configuração do sistema, consulte [extensão da linguagem Java no SQL Server 2019](extension-java.md). Para obter mais informações sobre requisitos de codificação, consulte [como chamar o Java no SQL Server](howto-call-java-from-sql.md).

+ SQL Server Management Studio ou outra ferramenta para a execução de T-SQL.

+ Java SE Development Kit (JDK) 1.10 no Windows ou JDK 1.8 no Linux.

Compilação de linha de comando usando **javac** é suficiente para este tutorial. 

## <a name="1---load-sample-data"></a>1 - carregar dados de exemplo

Primeiro, criar e preencher uma *revisa* de tabela com **ID** e **texto** colunas. Conectar-se ao SQL Server e execute o script a seguir para criar uma tabela:

```sql
DROP TABLE IF exists reviews;
GO
CREATE TABLE reviews(
    id int NOT NULL,
    "text" nvarchar(30) NOT NULL)

INSERT INTO reviews(id, "text") VALUES (1, 'AAA BBB CCC DDD EEE FFF')
INSERT INTO reviews(id, "text") VALUES (2, 'GGG HHH III JJJ KKK LLL')
INSERT INTO reviews(id, "text") VALUES (3, 'MMM NNN OOO PPP QQQ RRR')
GO
```

## <a name="2---class-ngramjava"></a>2 - classe Ngram.java

Comece criando a classe principal. Este é o primeiro de três classes.

Nesta etapa, crie uma classe chamada **Ngram.java** e copie o seguinte código Java para esse arquivo. 


```java
//We will package our classes in a package called pkg
//Packages are option in Java-SQL, but required for this sample.
package pkg;

import java.util.List;
import java.util.stream.Collectors;
import java.util.stream.IntStream;

public class Ngram {

    //Required: This is only required if you are passing data in @input_data_1
    //from SQL Server in sp_execute_external_script
    public static int[] inputDataCol1 = new int[1];
    public static String[] inputDataCol2 = new String[1];

    //Required: Input null map. Size just needs to be set to "1"
    public static boolean[][] inputNullMap = new boolean[1][1];

    //Required: Output data columns returned back to SQL Server
    public static int[] outputDataCol1;
    public static String[] outputDataCol2;

    //Required: Output null map. Is populated with true or false values 
    //to indicate nulls
    public static boolean[][] outputNullMap;

    //Optional: This is only required if parameters are passed with @params
    // from SQL Server in sp_execute_external_script
    // n is giving us the size of ngram substrings
    public static int param1;

    //Optional: The number of rows we will be returning
    public static int numberOfRows;

    //Required: Number of output columns returned
    public static short numberOfOutputCols;

    /*Java main method - Only for testing purposes outside of SQL Server
    public static void main(String... args) {
        //getNGrams();
    }*/

    //This is the method we will be calling from SQL Server
    public static void getNGrams() {

        System.out.println("inputDataCol1.length= "+ inputDataCol1.length);
        if (inputDataCol1.length == 0 ) {
            // TODO: Set empty return
            return;
        }
        //Using a stream to "loop" over the input data inputDataCol1.length. You can also use a for loop for this.
        final List<InputRow> inputDataSet = IntStream.range(0, inputDataCol1.length)
                .mapToObj(i -> new InputRow(inputDataCol1[i], inputDataCol2[i]))
                .collect(Collectors.toList());


        //Again, we are using a stream to loop over data
        final List<OutputRow> outputDataSet = inputDataSet.stream()
                // Generate ngrams of size n for each incoming string
                // Each invocation of ngrams returns a list. flatMap flattens
                // the resulting list-of-lists to a flat list.
                .flatMap(inputRow -> ngrams(param1, inputRow.text).stream().map(s -> new OutputRow(inputRow.id, s)))
                .collect(Collectors.toList());

        //Print the outputDataSet
        System.out.println(outputDataSet);

        //Set the number of rows and columns we will be returning
        numberOfOutputCols = 2;
        numberOfRows = outputDataSet.size();
        outputDataCol1 = new int[numberOfRows]; // ID column
        outputDataCol2 = new String[numberOfRows]; //The ngram column
        outputNullMap = new boolean[2][numberOfRows];// output null map

        //Since we don't have any null values, we will populate all values in the outputNullMap to false
        IntStream.range(0, numberOfRows).forEach(i -> {
            final OutputRow outputRow = outputDataSet.get(i);
            outputDataCol1[i] = outputRow.id;
            outputDataCol2[i] = outputRow.ngram;
            outputNullMap[0][i] = false;
            outputNullMap[1][i] = false;
        });
    }

    // Example: ngrams(3, "abcde") = ["abc", "bcd", "cde"].
    private static List<String> ngrams(int n, String text) {
        return IntStream.range(0, text.length() - n + 1)
                .mapToObj(i -> text.substring(i, i + n))
                .collect(Collectors.toList());
    }
}
```

## <a name="3---class-inputrowjava"></a>3 - classe InputRow.java

Criar uma segunda classe chamada **InputRow.java**, composto de código a seguir e salvo no mesmo local como **Ngram.java**.

```java
package pkg;

//This object represents one input row
public class InputRow {
    public final int id;
    public final String text;

    public InputRow(final int id, final String text) {
        this.id = id;
        this.text = text;
    }
}
```

## <a name="4---class-outputrowjava"></a>4 - classe OutputRow.java

A terceira e última classe é chamada **OutputRow.java**. Copie o código e salve como OutputRow.java no mesmo local que os outros.

```java
package pkg;

//This object represents one output row
public class OutputRow {
    public final int id;
    public final String ngram;

    public OutputRow(final int id, final String ngram) {
        this.id = id;
        this.ngram = ngram;
    }

    @Override
    public String toString() { return id + ":" + ngram; }
}
```

## <a name="5---compile"></a>5 - compilação

Uma vez que suas classes estiver prontos, execute javac para compilá-los em arquivos. "class" (`javac Ngram.java InputRow.java OutputRow.java`). Você deve obter os três arquivos. class para este exemplo (Ngram.class, InputRow.class e OutputRow.class).

Colocar o código compilado em uma subpasta chamada "pkg" no local de classpath. Se você estiver trabalhando em uma estação de trabalho de desenvolvimento, essa etapa é onde você copiar os arquivos para o computador do SQL Server.

O classpath é o local do código compilado. Por exemplo, no Linux, se for o classpath '/ home/myclasspath /', em seguida, os arquivos. class devem ser em '/ myclasspath/home/pkg'. No script de exemplo na etapa 7, o CLASSPATH fornecido no sp_execute_external_script é ' / home/myclasspath /' (supondo que o Linux). 

No Windows, é recomendável usar uma pasta relativamente superficial estrutura, um ou dois níveis abaixo, para simplificar a permissões. Por exemplo, o caminho de classe pode parecer com 'C:\myJavaCode' com uma subpasta chamada '\pkg' que contém as classes compiladas. 

Para obter mais informações sobre o classpath, consulte [definir o CLASSPATH](howto-call-java-from-sql.md#set-classpath). 

### <a name="using-jar-files"></a>Usando arquivos. jar

Se você planeja empacotar suas classes e as dependências em arquivos. jar, forneça o caminho completo para o arquivo. jar no parâmetro CLASSPATH sp_execute_external_script. Por exemplo, se o arquivo jar é chamado 'ngram.jar', o CLASSPATH será ' / home/myclasspath/ngram.jar' no Linux.

## <a name="6---set-permissions"></a>6 - definir permissões

Execução do script é bem-sucedido somente se as identidades de processo tem acesso ao seu código. 

### <a name="on-linux"></a>No Linux

Conceder permissões de leitura/execução no classpath para o **mssql_satellite** usuário.

### <a name="on-windows"></a>No Windows

Conceda as permissões 'Leitura e Execute' **SQLRUserGroup** e o **todos os pacotes de aplicativos** SID na pasta que contém o código Java compilado. 

Toda a árvore deve ter as permissões, da raiz pai para a última subpasta. 
 
1. Clique com botão direito na pasta (por exemplo, ' C:\myJavaCode'), escolha **propriedades** > **segurança**.
2. Clique em **Editar**.
3. Clique em **Adicionar**.
4. Na **selecionar usuários, computador, contas de serviço ou grupos**:
   + Clique em **tipos de objetos** e verifique se *princípios de segurança internas* e *grupos* estão selecionados.
   + Clique em **locais** para selecionar o nome do computador local na parte superior da lista.
5. Insira **SQLRUserGroup**, verifique o nome e, em seguida, clique em Okey para adicionar o grupo.
6. Insira **todos os pacotes de aplicativos**, verifique o nome e, em seguida, clique em Okey para adicionar. Se o nome não for resolvido, reveja a etapa de locais. O SID é local para seu computador.

Verifique se que ambas as identidades de segurança tem as permissões 'Ler e executar' na pasta e subpasta "pkg".

<a name="call-method"></a>

## <a name="7---call-getngrams"></a>7 - chamada *getNgrams()*

Para chamar o código do SQL Server, especifique o método de Java **getNgrams()** no parâmetro de sp_execute_external_script "script". Esse método pertence a um pacote denominado "pkg" e um arquivo de classe chamado **Ngram.java**.

Este exemplo passa o parâmetro de caminho de classe para fornecer o caminho para os arquivos Java. Ele também usa "params" para passar um parâmetro para a classe de Java. Certifique-se de que classpath não exceder 30 caracteres. Se isso acontecer, aumente o valor no script a seguir.

+ No Linux, execute o seguinte código no SQL Server Management Studio ou outra ferramenta usada para a execução de Transact-SQL. 

+ No Windows, altere **@myClassPath** para N'C:\myJavaCode\' (supondo que é a pasta pai de \pkg) antes de executar a consulta no SQL Server Management Studio ou outra ferramenta.

```sql
DECLARE @myClassPath nvarchar(50)
DECLARE @n int 
--This is where you store your classes or jars.
--Update this to your own classpath
SET @myClassPath = N'/home/myclasspath/'
--This is the size of the ngram
SET @n = 3
EXEC sp_execute_external_script
  @language = N'Java'
, @script = N'pkg.Ngram.getNGrams'
, @input_data_1 = N'SELECT id, text FROM reviews'
, @parallel = 0
, @params = N'@CLASSPATH nvarchar(30), @param1 INT'
, @CLASSPATH = @myClassPath
, @param1 = @n
with result sets ((ID int, ngram varchar(20)))
GO
```

### <a name="results"></a>Resultados

Depois de executar a chamada, você deve obter um conjunto que mostra as duas colunas de resultados:

![Os resultados do exemplo de Java](../media/java/java-sample-results.png "resultados de exemplo")

### <a name="if-you-get-an-error"></a>Se você receber um erro

Elimine problemas relacionados ao classpath. 

+ Classpath deve consistir em pasta pai e todas as subpastas, mas não a subpasta "pkg". Enquanto a subpasta pkg deve existir, ele não deveria para ser no valor de classpath especificado no procedimento armazenado.

+ A subpasta "pkg" deve conter o código compilado para todas as três classes.

+ O comprimento do caminho de classe não pode exceder o valor declarado (`DECLARE @myClassPath nvarchar(50)`). Se isso acontecer, o caminho será truncado para os primeiros 50 caracteres e seu código compilado não será carregado. Você pode fazer um `SELECT @myClassPath` para verificar o valor. Aumente o comprimento, se não for suficiente 50 caracteres. 

+ Por fim, verifique as permissões no *cada* pasta da raiz na subpasta "pkg", para garantir que as identidades de segurança que executa o processo externo tenham permissão para ler e executar seu código.

## <a name="see-also"></a>Confira também

+ [Como chamar o Java no SQL Server](howto-call-java-from-sql.md)
+ [Extensões de Java no SQL Server](extension-java.md)
+ [Tipos de dados Java e o SQL Server](java-sql-datatypes.md)
