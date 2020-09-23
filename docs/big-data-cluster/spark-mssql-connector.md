---
title: Usar o Conector do Apache Spark para SQL Server e Azure SQL
titleSuffix: SQL Server big data clusters
description: Saiba como usar o Conector do Apache Spark para SQL Server e SQL do Azure para ler e gravar no SQL Server.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mikeray
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: machine-learning-bdc
ms.openlocfilehash: 454d5fadaa88d645e9d1c2feec2c9d87c2af29c9
ms.sourcegitcommit: 331b8495e4ab37266945c81ff5b93d250bdaa6da
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88645497"
---
# <a name="use-the-apache-spark-connector-for-sql-server-and-azure-sql"></a>Usar o Conector do Apache Spark para SQL Server e Azure SQL

O [Conector do Apache Spark para SQL Server e Azure SQL](https://github.com/microsoft/sql-spark-connector) é um conector de alto desempenho que permite usar dados transacionais na análise de Big Data e persiste resultados para consultas ou relatórios ad hoc. O conector permite que você use qualquer banco de dados SQL, local ou na nuvem, como uma fonte de dados de entrada ou coletor de dados de saída para trabalhos do Spark. O conector usa APIs de gravação em massa do SQL Server. Os parâmetros de gravação em massa podem ser passados como parâmetros opcionais pelo usuário e passados no estado em que se encontram pelo conector para a API subjacente. Confira mais informações sobre operações de gravação em massa em [Como usar cópia em massa com o JDBC Driver]( ../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md#sqlserverbulkcopyoptions).

O conector é incluído por padrão nos Clusters de Big Data do SQL Server.

Saiba mais sobre o conector no [repositório de software livre](https://github.com/microsoft/sql-spark-connector). Confira exemplos em [amostras](https://github.com/microsoft/sql-spark-connector/tree/master/samples).

## <a name="write-to-a-new-sql-table"></a>Gravar em uma nova Tabela SQL

>[!CAUTION]
> No modo `overwrite`, o conector primeiro descartará a tabela se ela já existir no banco de dados por padrão. Use essa opção com cuidado para evitar perda de dados inesperada.
> 
> Ao usar o modo `overwrite`, os índices serão perdidos na recriação da tabela se você não usar a opção `truncate`. Por exemplo, uma tabela columnstore se torna um heap. Se você quiser manter a indexação existente, especifique também a opção `truncate` com o valor `true`. Por exemplo `.option("truncate",true)`

```python
server_name = "jdbc:sqlserver://{SERVER_ADDR}"
database_name = "database_name"
url = server_name + ";" + "databaseName=" + database_name + ";"

table_name = "table_name"
username = "username"
password = "password123!#" # Please specify password here

try:
  df.write \
    .format("com.microsoft.sqlserver.jdbc.spark") \
    .mode("overwrite") \
    .option("url", url) \
    .option("dbtable", table_name) \
    .option("user", username) \
    .option("password", password) \
    .save()
except ValueError as error :
    print("Connector write failed", error)
```

## <a name="append-to-sql-table"></a>Anexar à Tabela SQL
```python
try:
  df.write \
    .format("com.microsoft.sqlserver.jdbc.spark") \
    .mode("append") \
    .option("url", url) \
    .option("dbtable", table_name) \
    .option("user", username) \
    .option("password", password) \
    .save()
except ValueError as error :
    print("Connector write failed", error)
```

## <a name="specify-the-isolation-level"></a>Especificar o nível de isolamento

Por padrão, o conector usará o nível de isolamento READ_COMMITTED ao executar a inserção em massa no banco de dados. Se você quiser substituir por outro nível de isolamento, use a opção `mssqlIsolationLevel`, conforme mostrado abaixo.
```python
    .option("mssqlIsolationLevel", "READ_UNCOMMITTED") \
```

## <a name="read-from-sql-table"></a>Ler da Tabela SQL

```python
jdbcDF = spark.read \
        .format("com.microsoft.sqlserver.jdbc.spark") \
        .option("url", url) \
        .option("dbtable", table_name) \
        .option("user", username) \
        .option("password", password).load()
```

## <a name="non-active-directory-mode"></a>Modo não Active Directory

Na segurança do modo não Active Directory, cada usuário tem um nome de usuário e uma senha que devem ser fornecidos como parâmetros durante a instanciação do conector para executar leituras e/ou gravações.

Um exemplo de instanciação do conector para o modo não Active Directory é apresentado abaixo. Antes de executar o script, substitua `?` pelo valor de sua conta.

```python
# Note: '?' is a placeholder for a necessary user-specified value
connector_type = "com.microsoft.sqlserver.jdbc.spark" 

url = "jdbc:sqlserver://master-p-svc;databaseName=?;"
writer = df.write \ 
   .format(connector_type)\ 
   .mode("overwrite") 
   .option("url", url) \ 
   .option("user", ?) \ 
   .option("password",?) 
writer.save() 
```

## <a name="active-directory-mode"></a>Modo do Active Directory

Na segurança do modo Active Directory, depois que um usuário tiver gerado um arquivo de tecla TAB, ele precisará fornecer `principal` e `keytab` como parâmetros durante a instanciação do conector.

Nesse modo, o driver carrega o arquivo keytab nos respectivos contêineres do executor. Em seguida, os executores usam o nome da entidade de segurança e keytab para gerar um token que é usado para criar um conector JDBC para leitura/gravação.

Um exemplo de instanciação do conector para o modo Active Directory é apresentado abaixo. Antes de executar o script, substitua `?` pelo valor de sua conta.

```python
# Note: '?' is a placeholder for a necessary user-specified value
connector_type = "com.microsoft.sqlserver.jdbc.spark"

url = "jdbc:sqlserver://master-p-svc;databaseName=?;integratedSecurity=true;authenticationScheme=JavaKerberos;" 
writer = df.write \ 
   .format(connector_type)\ 
   .mode("overwrite") 
   .option("url", url) \ 
   .option("principal", ?) \ 
   .option("keytab", ?)   

writer.save() 
```

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre clusters de Big Data, confira [Como implantar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] no Kubernetes](deployment-guidance.md)

Tem recomendações de comentários ou recursos para Clusters de Big Data do SQL Server? [Deixe-nos uma observação nos comentários sobre Clusters de Big Data do SQL Server](https://aka.ms/sql-server-bdc-feedback).
