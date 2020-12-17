---
title: Chamar o runtime Java
titleSuffix: SQL Server Language Extensions
description: Saiba como chamar classes Java de procedimentos armazenados do SQL Server usando a Extensão da Linguagem do SQL Server.
author: dphansen
ms.author: davidph
ms.date: 06/25/2020
ms.topic: how-to
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15'
ms.openlocfilehash: 2d62bb52d114c819dbd7de7e9244d50c27bcf248
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97471767"
---
# <a name="how-to-call-the-java-runtime-in-sql-server-language-extensions"></a>Como chamar o runtime Java nas Extensões de Linguagem do SQL Server
[!INCLUDE [SQL Server 2019 and later](../../includes/applies-to-version/sqlserver2019.md)]

As [Extensões de Linguagem do SQL Server](../language-extensions-overview.md) usam o procedimento armazenado do sistema [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) como a interface para chamar o runtime do Java. 

Este artigo de instruções explica detalhes de implementação para classes e métodos Java executados no SQL Server.

## <a name="where-to-place-java-classes"></a>Onde posicionar classes Java

Há dois métodos para chamar classes Java no SQL Server:

1. Coloque os arquivos **.class** ou **.jar** no [classpath do Java](#classpath). 

2. Faça upload de classes compiladas em um arquivo **.jar** e outras dependências no banco de dados usando a DDL da [biblioteca externa](#external-library). 

> [!NOTE]
> Como uma recomendação geral, use arquivos **.jar** e não arquivos **.class** individuais. Essa é uma prática comum em Java e facilitará a experiência geral. Confira também, [Como criar um arquivo jar com base em arquivos de classe](create-a-java-jar-file-from-class-files.md).

<a name="classpath"></a>

## <a name="use-classpath"></a>Usar Classpath

### <a name="basic-principles"></a>Princípios básicos

Veja a seguir alguns princípios básicos ao executar o Java no SQL Server.

* As classes Java personalizadas compiladas devem existir em arquivos **.class** ou **.jar** no classpath do Java. O [parâmetro CLASSPATH](#set-classpath) fornece o caminho para os arquivos Java compilados. 

* O método Java que você está chamando deve ser fornecido no parâmetro do **script** no procedimento armazenado.

* Se a classe pertencer a um pacote, o **packageName** deverá ser fornecido.

* **params** é usado para passar parâmetros para uma classe Java. Não há suporte para a chamada de um método que requer argumentos. Portanto, os parâmetros são a única maneira de passar valores de argumento para seu método. 

> [!NOTE]
> Esta observação reitera operações com e sem suporte específicas para Java no SQL Server 2019 versão Release Candidate 1.
> * No procedimento armazenado, há suporte para parâmetros de entrada. Não há para parâmetros de saída.

### <a name="call-java-class"></a>Chamar classes Java

O procedimento armazenado do sistema [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) é a interface usada para chamar o runtime do Java. O exemplo a seguir mostra um `sp_execute_external_script` que usa a extensão do Java e parâmetros para especificar o caminho, o script e o código personalizado.

> [!NOTE]
> Observe que você não precisa definir qual método chamar. Por padrão, um método chamado **execute** é chamado. Isso significa que você precisa seguir o [SDK de Extensibilidade para Java no SQL Server](extensibility-sdk-java-sql-server.md) e implementar um método execute em sua classe Java.

```sql
DECLARE @param1 int
SET @param1 = 3

EXEC sp_execute_external_script
  @language = N'Java'
, @script = N'<packageName>.<ClassName>'
, @input_data_1 = N'<Input Query>'
, @param1 = @param1
```

<a name="set-classpath"></a>

### <a name="set-classpath"></a>Definir CLASSPATH

Depois de ter compilado sua classe ou classes Java e criado um arquivo jar em sua classpath do Java, você terá duas opções para fornecer o classpath para a extensão de Java do SQL Server:

1. Usar bibliotecas externas

    A opção mais fácil é fazer o SQL Server encontrar automaticamente suas classes criando bibliotecas externas e apontando a biblioteca para um jar. [Usar bibliotecas externas para Java](#external-library)

2. Registrar uma variável de ambiente do sistema

    Você pode criar uma variável de ambiente do sistema e fornecer os caminhos para o arquivo jar que contém as classes. Crie uma variável de ambiente do sistema chamada **CLASSPATH**.

<a name="external-library"></a>

## <a name="use-external-library"></a>Usar biblioteca externa

No SQL Server 2019 versão Release Candidate 1, você pode usar bibliotecas externas para a linguagem Java no Windows e Linux. Você pode compilar suas classes em um arquivo .jar e fazer upload do arquivo .jar e de outras dependências no banco de dados usando a DDL [CREATE EXTERNAL LIBRARY](../../t-sql/statements/create-external-library-transact-sql.md).

Exemplo de como fazer upload de um arquivo .jar com a biblioteca externa:

```sql 
CREATE EXTERNAL LIBRARY myJar
FROM (CONTENT = '<local path to .jar file>') 
WITH (LANGUAGE = 'Java'); 
GO
```

Ao criar uma biblioteca externa, o SQL Server terá automaticamente acesso a classes Java e não precisará definir nenhuma permissão especial como o classpath.

Exemplo de chamar um método em uma classe de um pacote carregado como uma biblioteca externa:

```sql
EXEC sp_execute_external_script
  @language = N'Java'
, @script = N'MyPackage.MyCLass'
, @input_data_1 = N'SELECT * FROM MYTABLE'
with result sets ((column1 int))
```

Para obter mais informações, confira [CREATE EXTERNAL LIBRARY](../../t-sql/statements/create-external-library-transact-sql.md).

## <a name="loopback-connection-to-sql-server"></a>Conexão de loopback para o SQL Server

Use uma conexão de loopback para se conectar novamente ao SQL Server por JDBC a fim de ler ou gravar dados de um Java executado de `sp_execute_external_script`. Você poderá usar isso quando não for possível usar os argumentos **InputDataSet** e **OutputDataSet** de `sp_execute_external_script`.
Para fazer uma conexão de loopback no Windows, use o seguinte exemplo:

```
jdbc:sqlserver://localhost:1433;databaseName=Adventureworks;integratedSecurity=true;
``` 

Para fazer uma conexão de loopback no Linux, o driver JDBC requer três propriedades de conexão definidas no seguinte certificado:

[Autenticação de certificado do cliente](https://github.com/microsoft/mssql-jdbc/wiki/Client-Certificate-Authentication-for-Loopback-Scenarios)


## <a name="next-steps"></a>Próximas etapas

+ [Tutorial: Pesquisar uma cadeia de caracteres usando expressões regulares em Java](../tutorials/search-for-string-using-regular-expressions-in-java.md)