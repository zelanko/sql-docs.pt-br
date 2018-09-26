---
title: Como chamar Java do SQL | Microsoft Docs
description: Saiba como chamar classes Java de procedimentos armazenados do SQL Server usando a extensão no SQL Server 2019 da linguagem de programação Java.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/24/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 08af5a18b827c783515ecd3b4ba4a802c3472f93
ms.sourcegitcommit: b7fd118a70a5da9bff25719a3d520ce993ea9def
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2018
ms.locfileid: "46714866"
---
# <a name="how-to-call-java-from-sql-server-2019"></a>Como chamar Java de 2019 do SQL Server

Ao usar o [extensão da linguagem Java](extension-java.md), o [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) sistema, procedimento armazenado é a interface usada para chamar o tempo de execução do Java. Permissões no banco de dados se aplicam à execução de código Java.

Este artigo explica os detalhes de implementação para classes Java e métodos que executar no SQL Server. Quando estiver familiarizado com esses detalhes, examine os [exemplo de Java](java-first-sample.md) como sua próxima etapa.

## <a name="basic-principles"></a>Princípios básicos

* Compilado classes Java personalizadas devem existir em arquivos. class ou arquivos. jar no seu classpath de Java. O [parâmetro CLASSPATH](#set-classpath) fornece o caminho para os arquivos Java compilados. 

* O método de Java que você está chamando deve ser fornecido no parâmetro "script" no procedimento armazenado.

* Se a classe pertence a um pacote, "packageName" deve ser fornecido.

* "params" é usado para passar parâmetros para uma classe Java. Chamar um método que requer argumentos não for compatível, que torna a única maneira de passar valores de argumento para o seu método de parâmetros. 

> [!Note]
> Essa observação reafirmar compatíveis e sem suportadas operações específicas para Java no CTP 2.0.
> * No procedimento armazenado, há suporte para parâmetros de entrada. Não são parâmetros de saída.
> * Transmissão usando o parâmetro de sp_execute_external_script **@r_rowsPerRead** não tem suporte.
> * Usando o particionamento **@input_data_1_partition_by_columns** não tem suporte.
> * Uso de processamento paralelo  **@parallel= 1** tem suporte.

## <a name="call-spexecuteexternalscript"></a>Chamar sp_execute_external_script

O [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) sistema, procedimento armazenado é a interface usada para chamar o tempo de execução do Java. O exemplo a seguir mostra um sp_execute_external_script usando os parâmetros e a extensão de Java para especificar o caminho, o script e o seu código personalizado.

```sql
DECLARE @myClassPath nvarchar(30)
DECLARE @param1 int

SET @myClassPath = N'/<my path>/program.jar'
SET @param1 = 3

EXEC sp_execute_external_script
  @language = N'Java'
, @script = N'<packageName>.<ClassName>.<methodName>'
, @input_data_1 = N'<Input Query>
, @params = N'@CLASSPATH nvarchar(30), @param1 INT'
, @CLASSPATH = @myClassPath
, @param1 = @param1
```

<a name="set-classpath"></a>

## <a name="set-classpath"></a>Definir o CLASSPATH

Depois que você tiver compilado seu classe Java ou classes e colocado o arquivo (s). class ou arquivos. jar no seu classpath de Java, você tem duas opções para fornecer o classpath para a extensão de Java do SQL Server:

**Opção 1: Passar como um parâmetro**

É uma abordagem para especificar um caminho para o código compilado, definindo o CLASSPATH como um parâmetro de entrada para o procedimento de sp_execute_external_script. O [exemplo de Java](java-first-sample.md#call-method) demonstra essa técnica. Se você escolher essa abordagem e tiver vários caminhos, certifique-se de usar o separador de caminho é válido para o sistema operacional subjacente:

* No Linux, separe os caminhos no CLASSPATH com dois-pontos ":".
* No Windows, separe os caminhos no CLASSPATH com ponto e vírgula ";"

**Opção 2: Registrar uma variável do sistema**

Assim como você criou uma variável de sistema para os executáveis do JDK, você pode criar uma variável de sistema para caminhos de código. Para fazer isso, criou uma variável de ambiente do sistema chamada "CLASSPATH"

## <a name="class-requirements"></a>Requisitos de classe

Para o SQL Server para se comunicar com o tempo de execução do Java, você precisa implementar variáveis estáticas específicas em sua classe. SQL Server, em seguida, pode executar um método os dados de classe e o exchange do Java usando a extensão da linguagem Java.

> [!Note]
> Espere os detalhes de implementação para alterar em CTPs futuros, estamos trabalhando para melhorar a experiência para os desenvolvedores.

## <a name="method-requirements"></a>Requisitos do método
Para passar argumentos, use o **@param** parâmetro em sp_execute_external_script. O método em si não pode ter nenhum argumento. O tipo de retorno deve ser nulo.  

```java
public static void test()  {}
```

## <a name="data-inputs"></a>Entradas de dados 

Esta seção explica como enviar dados por push ao Java de uma consulta do SQL Server que usa **InputDataSet** em sp_execute_external_script.

Para cada coluna de entrada que sua consulta SQL envia por push para Java, você precisa declarar uma matriz.

### <a name="inputdatacol"></a>inputDataCol

Na versão atual da extensão de Java, o **inputDataColN** variável é necessária, onde *N* é o número da coluna. 

```java
public static <type>[] inputDataColN = new <type>[1]
```

Essas matrizes precisam ser inicializados (o tamanho da matriz deve ser maior que 0 e não precisa refletir o comprimento real da coluna).

Exemplo: `public static int[] inputDataCol1 = new int[1];`

Essas variáveis de matriz serão preenchidas com dados de entrada de uma consulta do SQL server antes da execução do programa Java que você está chamando.

### <a name="inputnullmap"></a>inputNullMap

Mapa nulo é usado pela extensão de saber quais valores são nulos. Essa variável será preenchida com informações sobre valores nulos pelo SQL Server antes da execução da função de usuário.

O usuário só precisa inicializar essa variável (e o tamanho da matriz deve ser maior que 0).

```java
public static boolean[][] inputNullMap = new boolean[1][1];
```

## <a name="data-outputs"></a>Saídas de dados 

Esta seção descreve **OutputDataSet**, os conjuntos de dados de saída retornado do Java, que você pode enviar para e manter no SQL Server.

> [!Note]
> Parâmetros de saída [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) não têm suporte nesta versão.

### <a name="outputdatacoln"></a>outputDataColN

Semelhante ao **inputDataSet**, para cada coluna de saída que seu programa Java envia para o SQL Server, você deve declarar uma variável de matriz. Todos os **outputDataCol** matrizes devem ter o mesmo tamanho. Você precisa certificar-se de que isso é inicializado no momento em que a execução de classe for concluída.

```java
public static <type>[] outputDataColN = new <type>[]
```

### <a name="numberofoutputcols"></a>numberofOutputCols

Defina essa variável como o número de colunas de dados de saída, que você espera ter quando a função de usuário conclui a execução.

```java
public static short numberofOutputCols = <expected number of output columns>;
```

### <a name="outputnullmap"></a>outputNullMap

Mapa nulo é usado pela extensão para indicar quais valores são nulos. É necessário, pois os tipos primitivos não dão suporte a nulo. Atualmente, também Exigimos que o mapa de nulo para tipos de cadeia de caracteres, mesmo que as cadeias de caracteres podem ser nulas. Valores nulos são indicados por "true".

Este NullMap deve ser preenchida com o número esperado de colunas e linhas que você está retornando para o SQL Server.

```java
public static boolean[][] outputNullMap
```

## <a name="next-steps"></a>Próximas etapas

+ [Exemplo de Java no SQL Server](java-first-sample.md)
+ [Tipos de dados Java e o SQL Server](java-sql-datatypes.md)
+ [Extensão da linguagem Java no SQL Server](extension-java.md)
