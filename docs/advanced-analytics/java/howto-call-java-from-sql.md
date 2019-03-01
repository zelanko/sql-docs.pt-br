---
title: Como chamar Java de SQL - serviços do SQL Server Machine Learning
description: Saiba como chamar classes Java de procedimentos armazenados do SQL Server usando a extensão no SQL Server 2019 da linguagem de programação Java.
ms.prod: sql
ms.technology: machine-learning
ms.date: 02/28/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 801ffe50ca83fbeda69a3172b5914d39373d643f
ms.sourcegitcommit: 2533383a7baa03b62430018a006a339c0bd69af2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57017752"
---
# <a name="how-to-call-java-from-sql-server-2019-preview"></a>Como chamar Java da visualização do SQL Server de 2019

Ao usar o [extensão da linguagem Java](extension-java.md), o [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) sistema, procedimento armazenado é a interface usada para chamar o tempo de execução do Java. Permissões no banco de dados se aplicam à execução de código Java.

Este artigo explica os detalhes de implementação para classes Java e métodos que executar no SQL Server. Quando estiver familiarizado com esses detalhes, examine os [exemplo de Java](java-first-sample.md) como sua próxima etapa.

Há dois métodos para chamar as classes Java no SQL Server:

1. Colocar os arquivos. class ou. jar na sua [classpath de Java](#classpath). Isso está disponível para Windows e Linux.

2. Carregar classes compiladas em um arquivo. jar e outras dependências no banco de dados usando o [biblioteca externa](#external-library) DDL. Essa opção está disponível para Windows somente no CTP 2.3. Suporte para Linux será adicionado em um CTP mais recente.

> [!NOTE]
> Como uma recomendação geral, use arquivos. jar e arquivos. class não individuais. Essa é uma prática comum em Java e facilitará a experiência geral. Consulte também: [Como criar um arquivo jar de arquivos de classe](extension-java.md#create-jar).

<a name="classpath"></a>

## <a name="classpath"></a>Classpath

### <a name="basic-principles"></a>Princípios básicos

* Compilado classes Java personalizadas devem existir em arquivos. class ou arquivos. jar no seu classpath de Java. O [parâmetro CLASSPATH](#set-classpath) fornece o caminho para os arquivos Java compilados. 

* O método de Java que você está chamando deve ser fornecido no parâmetro "script" no procedimento armazenado.

* Se a classe pertence a um pacote, "packageName" deve ser fornecido.

* "params" é usado para passar parâmetros para uma classe Java. Chamar um método que requer argumentos não for compatível, que torna a única maneira de passar valores de argumento para o seu método de parâmetros. 

> [!Note]
> Essa observação reafirmar compatíveis e sem suportadas operações específicas para Java no CTP 2. x.
> * No procedimento armazenado, há suporte para parâmetros de entrada. Não são parâmetros de saída.
> * Transmissão usando o parâmetro de sp_execute_external_script @r_rowsPerRead não tem suporte.
> * Usando o particionamento @input_data_1_partition_by_columns não tem suporte.
> * Uso de processamento paralelo @parallel= 1 é suportado.

### <a name="call-class"></a>Classe Call

Aplicável ao Windows e Linux, o [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) sistema, procedimento armazenado é a interface usada para chamar o tempo de execução do Java. O exemplo a seguir mostra um sp_execute_external_script usando os parâmetros e a extensão de Java para especificar o caminho, o script e o seu código personalizado.

```sql
DECLARE @myClassPath nvarchar(30)
DECLARE @param1 int

SET @myClassPath = N'/<my path>/program.jar'
SET @param1 = 3

EXEC sp_execute_external_script
  @language = N'Java'
, @script = N'<packageName>.<ClassName>.<methodName>'
, @input_data_1 = N'<Input Query>'
, @params = N'@CLASSPATH nvarchar(30), @param1 INT'
, @CLASSPATH = @myClassPath
, @param1 = @param1
```

<a name="set-classpath"></a>

### <a name="set-classpath"></a>Definir o CLASSPATH

Depois que você tiver compilado seu classe Java ou classes e colocado o arquivo (s). class ou arquivos. jar no seu classpath de Java, você tem duas opções para fornecer o classpath para a extensão de Java do SQL Server:

**Opção 1: Passar como um parâmetro**

É uma abordagem para especificar um caminho para o código compilado, definindo o CLASSPATH como um parâmetro de entrada para o procedimento de sp_execute_external_script. O [exemplo de Java](java-first-sample.md#call-method) demonstra essa técnica. Se você escolher essa abordagem e tiver vários caminhos, certifique-se de usar o separador de caminho é válido para o sistema operacional subjacente:

* No Linux, separe os caminhos no CLASSPATH com dois-pontos ":".
* No Windows, separe os caminhos no CLASSPATH com ponto e vírgula ";"

**Opção 2: Registre-se uma variável de sistema**

Assim como você criou uma variável de sistema para os executáveis do JDK, você pode criar uma variável de sistema para caminhos de código. Para fazer isso, criou uma variável de ambiente do sistema chamada "CLASSPATH"

<a name="external-library"></a>

## <a name="external-library"></a>Biblioteca externa

No SQL Server de 2019 CTP 2.3, você pode usar bibliotecas externas para o idioma de Java no Windows. A mesma funcionalidade estará disponível no Linux em um CTP futuro. Você pode compilar suas classes em um arquivo. jar e carregue o arquivo. jar e outras dependências no banco de dados usando o [CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) DDL.

Exemplo de como carregar um arquivo. jar com biblioteca externa:

```sql 
CREATE EXTERNAL LIBRARY myJar
FROM (CONTENT = '<local path to .jar file>') 
WITH (LANGUAGE = 'Java'); 
GO
```

Criando uma biblioteca externa, você não precisa fornecer um [classpath](#classpath) na chamada a sp_execute_external_script. SQL Server terão acesso às classes Java automaticamente e você não precisará definir permissões especiais ao classpath.

Exemplo de como chamar um método em uma classe de um pacote é carregado como uma biblioteca externa:

```sql
EXEC sp_execute_external_script
  @language = N'Java'
, @script = N'MyPackage.MyCLass.myMethod'
, @input_data_1 = N'SELECT * FROM MYTABLE'
with result sets ((column1 int))
```

Para obter mais informações, consulte [CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql).

## <a name="class-requirements"></a>Requisitos de classe

Para o SQL Server para se comunicar com o tempo de execução do Java, você precisa implementar variáveis estáticas específicas em sua classe. SQL Server, em seguida, pode executar um método os dados de classe e o exchange do Java usando a extensão da linguagem Java.

> [!Note]
> Espere os detalhes de implementação para alterar em CTPs futuros, estamos trabalhando para melhorar a experiência para os desenvolvedores.

## <a name="method-requirements"></a>Requisitos do método
Para passar argumentos, use o @param parâmetro em sp_execute_external_script. O método em si não pode ter nenhum argumento. O tipo de retorno deve ser nulo.  

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
