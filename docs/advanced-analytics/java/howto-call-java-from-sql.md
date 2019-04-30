---
title: Como chamar Java de SQL - serviços do SQL Server Machine Learning
description: Saiba como chamar classes Java de procedimentos armazenados do SQL Server usando a extensão no SQL Server 2019 da linguagem de programação Java.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/23/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: a75878ccc4f14d03f84102dd48bfd43a6e04daea
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63473559"
---
# <a name="how-to-call-java-from-sql-server-2019-preview"></a>Como chamar Java da visualização do SQL Server de 2019

Ao usar o [extensão da linguagem Java](extension-java.md), o [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) sistema, procedimento armazenado é a interface usada para chamar o tempo de execução do Java. Permissões no banco de dados se aplicam à execução de código Java.

Este artigo explica os detalhes de implementação para classes Java e métodos que executar no SQL Server. Quando estiver familiarizado com esses detalhes, examine os [exemplo de Java](java-first-sample.md) como sua próxima etapa.

Há dois métodos para chamar as classes Java no SQL Server:

1. Colocar os arquivos. class ou. jar na sua [classpath de Java](#classpath). Isso está disponível para Windows e Linux.

2. Carregar classes compiladas em um arquivo. jar e outras dependências no banco de dados usando o [biblioteca externa](#external-library) DDL. Essa opção está disponível para Windows e Linux do CTP 2.4.

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

### <a name="call-java-class"></a>Chame a classe de Java

Aplicável ao Windows e Linux, o [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) sistema, procedimento armazenado é a interface usada para chamar o tempo de execução do Java. O exemplo a seguir mostra um sp_execute_external_script usando os parâmetros e a extensão de Java para especificar o caminho, o script e o seu código personalizado.

> [!NOTE]
> Observe que você não precisa definir o método a ser chamado. Por padrão, um método chamado **executar** é chamado. Isso significa que você precisa seguir o SDK e implementar um método execute em sua classe de Java.

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

### <a name="set-classpath"></a>Definir o CLASSPATH

Uma vez você tiver compilado seu classe Java ou classes e criado um arquivo jar no seu classpath de Java, você tem duas opções para fornecer o classpath para a extensão de Java do SQL Server:

**Opção 1: Usar bibliotecas externas** a opção mais fácil é fazer com que o SQL Server localizar automaticamente suas classes de criação de bibliotecas externas e apontando a biblioteca para um jar. [Usar bibliotecas externas para Java](howto-call-java-from-sql.md#external-library)

**Opção 2: Registre-se uma variável de ambiente do sistema**

Assim como você criou uma variável de ambiente do sistema para o tempo de execução do Java, você pode criar uma variável de ambiente do sistema e fornecer os caminhos para o arquivo jar que contém as classes. Para fazer isso, você precisará criar uma variável de ambiente do sistema chamada "CLASSPATH".

<a name="external-library"></a>

## <a name="external-library"></a>Biblioteca externa

No SQL Server de 2019 CTP 2.4, você pode usar bibliotecas externas para o idioma de Java no Windows e Linux. Você pode compilar suas classes em um arquivo. jar e carregue o arquivo. jar e outras dependências no banco de dados usando o [CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) DDL.

Exemplo de como carregar um arquivo. jar com biblioteca externa:

```sql 
CREATE EXTERNAL LIBRARY myJar
FROM (CONTENT = '<local path to .jar file>') 
WITH (LANGUAGE = 'Java'); 
GO
```

Criando uma biblioteca externa, SQL Server terão acesso às classes Java automaticamente e não é necessário definir permissões especiais ao classpath.

Exemplo de como chamar um método em uma classe de um pacote é carregado como uma biblioteca externa:

```sql
EXEC sp_execute_external_script
  @language = N'Java'
, @script = N'MyPackage.MyCLass'
, @input_data_1 = N'SELECT * FROM MYTABLE'
with result sets ((column1 int))
```

Para obter mais informações, consulte [CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql).

## <a name="next-steps"></a>Próximas etapas

+ [Exemplo de Java no SQL Server](java-first-sample.md)
+ [Tipos de dados Java e o SQL Server](java-sql-datatypes.md)
+ [Extensão da linguagem Java no SQL Server](extension-java.md)
