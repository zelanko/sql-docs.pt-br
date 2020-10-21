---
title: Conector do Apache Spark para SQL Server
description: Saiba como usar o conector de Apache Spark para SQL Server.
ms.custom: ''
ms.date: 08/31/2020
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rajmera3
ms.author: raajmera
ms.reviewer: mikeray
ms.openlocfilehash: 059ecfb25389de1be0f8636a868e81e621e57bac
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91867241"
---
# <a name="apache-spark-connector-sql-server--azure-sql"></a>Conector do Apache Spark: SQL Server e SQL do Azure

O Conector do Apache Spark para SQL Server e Azure SQL é um conector de alto desempenho que permite usar dados transacionais na análise de Big Data e persiste resultados para consultas ou relatórios ad hoc. O conector permite que você use qualquer banco de dados SQL, local ou na nuvem, como uma fonte de dados de entrada ou coletor de dados de saída para trabalhos do Spark.

Esta biblioteca contém o código-fonte para o conector do Apache Spark para SQL Server e SQL do Azure.

O [Apache Spark](https://spark.apache.org/) é um mecanismo de análise unificado para processamento de dados em grande escala.

Importe o conector para o seu projeto por meio das coordenadas do Maven: `com.microsoft.azure:spark-mssql-connector:1.0.0`. Crie também o conector com base na origem ou baixe o JAR da seção Versão no GitHub. Para obter as informações mais recentes sobre o conector, confira [Repositório GitHub do conector do SQL Spark](https://github.com/microsoft/sql-spark-connector).

## <a name="supported-features"></a>Recursos com suporte

* Suporte para todas as associações do Spark (Scala, Python, R)
* Suporte à Guia Chave do AD (Active Directory) e autenticação básica
* Suporte à gravação do `dataframe` reordenado
* Suporte para gravação em instância única do SQL Server e Pool de Dados em Clusters de Big Data do SQL Server
* Suporte a conector confiável para instância única do SQL Server

| Componente                            | Versões com suporte              |
|--------------------------------------|---------------------------------|
| Apache Spark                         | 2.4.5 (Spark 3.0 sem suporte) |
| Scala                                | 2,11                            |
| Microsoft JDBC Driver para SQL Server | 8.2                             |
| Microsoft SQL Server                 | SQL Server 2008 ou posterior        |
| Bancos de Dados SQL do Azure                  | Com suporte                       |

> [!NOTE]
> O uso do Azure Synapse Analytics (Azure SQL DW) não é testado com esse conector. Embora possa funcionar, pode haver consequências indesejadas.

### <a name="supported-options"></a>Opções Suportadas
O Conector do Apache Spark para SQL Server e SQL do Azure dá suporte às opções definidas aqui: [JDBC do DataSource SQL](https://spark.apache.org/docs/latest/sql-data-sources-jdbc.html)

Além disso, há suporte para as opções a seguir

| Opção | Padrão | Descrição |
| --------- | ------------------ | ------------------------------------------ |
| `reliabilityLevel` | `BEST_EFFORT` | `BEST_EFFORT` ou `NO_DUPLICATES`. `NO_DUPLICATES` implementa uma inserção confiável em cenários de reinicialização do executor |
| `dataPoolDataSource` | `none` | `none` implica que o valor não está definido e o conector deve fazer a gravação na instância única do SQL Server. Defina esse valor como o nome da fonte de dados para gravar uma tabela de pool de dados em Clusters de Big Data|
| `isolationLevel` | `READ_COMMITTED` | Especificar o nível de isolamento |
| `tableLock` | `false` | Implementa uma inserção com a opção `TABLOCK` para melhorar o desempenho de gravação |
| `schemaCheckEnabled` | `true` | Desabilita a verificação estrita de quadro de dados e esquema de tabela SQL quando definido como falso |

Outras [opções de cópia em massa](../jdbc/using-bulk-copy-with-the-jdbc-driver.md#sqlserverbulkcopyoptions) podem ser definidas como opções no `dataframe` e serão passadas para APIs `bulkcopy` na gravação

## <a name="performance-comparison"></a>Comparação de desempenho

O Conector do Apache Spark para SQL Server e Azure SQL é até 15x mais rápido do que o conector JDBC genérico para gravar no SQL Server. As características de desempenho variam em termos de tipo, volume de dados e opções usadas, podendo apresentar variações entre execuções. Os resultados de desempenho a seguir são o tempo necessário para substituir uma tabela SQL por 143,9 milhões de linhas em um `dataframe` do Spark. O `dataframe` do Spark é construído lendo a tabela HDFS `store_sales` gerada usando [Benchmark TPCDS do Spark](https://github.com/databricks/spark-sql-perf). O tempo para ler `store_sales` para `dataframe` foi excluído. A média dos resultados é calculada em três execuções.

| Tipo de Conector | Opções | Descrição |  Tempo para gravar |
| --------- | ------------------ | -------------------------------------| ---------- |
| `JDBCConnector` | Padrão | Conector JDBC genérico com opções padrão |  1\.385 segundos |
| `sql-spark-connector` | `BEST_EFFORT` | Melhor esforço `sql-spark-connector` com opções padrão |580 segundos |
| `sql-spark-connector` | `NO_DUPLICATES ` | `sql-spark-connector` confiável | 709 segundos |
| `sql-spark-connector` | `BEST_EFFORT` + tabLock=true | Melhor esforço `sql-spark-connector` com o bloqueio de tabela habilitado | 72 segundos |
| `sql-spark-connector` | `NO_DUPLICATES ` + tabLock=true| `sql-spark-connector` confiável com o bloqueio de tabela habilitado| 198 segundos |

Config

- Spark config: num_executors = 20, executor_memory = '1664 m', executor_cores = 2
- Data Gen config: scale_factor=50, partitioned_tables=true
- Arquivo de dados `store_sales` com número de linhas 143.997.590

Ambiente

- CU5 do [Cluster de Big Data do SQL Server](../../big-data-cluster/release-notes-big-data-cluster.md)
- `master` + 6 nós
- Cada nó servidor geração 5, 512 GB de RAM, NVM de 4 TB por nó, NIC 10 GB

## <a name="commonly-faced-issues"></a>Problemas geralmente enfrentados

### `java.lang.NoClassDefFoundError: com/microsoft/aad/adal4j/AuthenticationException`

Esse problema surge com o uso de uma versão mais antiga do driver mssql (que agora está incluída nesse conector) em seu ambiente do hadoop. Se você usava o conector do Azure SQL anterior e está instalado manualmente os drivers nesse cluster para compatibilidade com o Azure Active Directory, é necessário remover esses drivers.

Etapas para corrigir o problema:

1. Se você estiver usando um ambiente Hadoop genérico, verifique e remova o mssql jar: `rm $HADOOP_HOME/share/hadoop/yarn/lib/mssql-jdbc-6.2.1.jre7.jar`. Se você está usando o Databricks, adicione um script de inicialização global ou de cluster para remover versões antigas do driver mssql da pasta `/databricks/jars` ou adicione essa linha a um script existente: `rm /databricks/jars/*mssql*`
2. Adicione os pacotes de `adal4j` e `mssql`. Por exemplo, você pode usar o Maven, mas qualquer forma deve funcionar. 

   > [!CAUTION]
   > Não instale o conector do SQL Spark dessa maneira.

1. Adicione a classe de driver à sua configuração de conexão. Por exemplo:

   ```csharp
   connectionProperties = {
     `Driver`: `com.microsoft.sqlserver.jdbc.SQLServerDriver`
   }`
   ```

Para obter mais informações e explicações, confira a resolução para [https://github.com/microsoft/sql-spark-connector/issues/26](https://github.com/microsoft/sql-spark-connector/issues/26#issuecomment-672006339).

## <a name="get-started"></a>Introdução

O Conector do Apache Spark para SQL Server e Azure SQL é baseado na API do Spark DataSourceV1 e na API em Massa do SQL Server e usa a mesma interface do conector JDBC Spark-SQL interno. Essa integração permite que você integre facilmente o conector e migre seus trabalhos do Spark simplesmente atualizando o parâmetro format com `com.microsoft.sqlserver.jdbc.spark`.

Para incluir o conector em seus projetos, baixe esse repositório e compile o jar usando SBT.

## <a name="write-to-a-new-sql-table"></a>Gravar em uma nova Tabela SQL

> [!WARNING]
> O modo `overwrite` primeiro descartará a tabela se ela já existir no banco de dados por padrão. Use essa opção com cuidado para evitar perda de dados inesperada.

Ao usar o modo `overwrite`, os índices serão perdidos na recriação da tabela se você não usar a opção `truncate`. , uma tabela columnstore agora seria um heap. Se você quiser manter a indexação existente, especifique também a opção `truncate` com o valor true. Por exemplo, `.option("truncate","true")`.

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

### <a name="append-to-sql-table"></a>Acrescentar à Tabela SQL

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

Por padrão, o conector usará o nível de isolamento `READ_COMMITTED` ao executar a inserção em massa no banco de dados. Se você quiser substituir o nível de isolamento, use a opção `mssqlIsolationLevel`, conforme mostrado abaixo.

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

## <a name="azure-active-directory-authentication"></a>Autenticação do Azure Active Directory

### <a name="python-example-with-service-principal"></a>Exemplo do Python com Entidade de Serviço

```python
context = adal.AuthenticationContext(authority)
token = context.acquire_token_with_client_credentials(resource_app_id_url, service_principal_id, service_principal_secret)
access_token = token["accessToken"]

jdbc_db = spark.read \
        .format("com.microsoft.sqlserver.jdbc.spark") \
        .option("url", url) \
        .option("dbtable", table_name) \
        .option("accessToken", access_token) \
        .option("encrypt", "true") \
        .option("hostNameInCertificate", "*.database.windows.net") \
        .load()
```

### <a name="python-example-with-active-directory-password"></a>Exemplo do Python com Senha do Active Directory

```python
jdbc_df = spark.read \
        .format("com.microsoft.sqlserver.jdbc.spark") \
        .option("url", url) \
        .option("dbtable", table_name) \
        .option("authentication", "ActiveDirectoryPassword") \
        .option("user", user_name) \
        .option("password", password) \
        .option("encrypt", "true") \
        .option("hostNameInCertificate", "*.database.windows.net") \
        .load()
```

Uma dependência necessária deve ser instalada para autenticar usando o Active Directory.

Para **Scala,** o artefato `_com.microsoft.aad.adal4j_` precisará ser instalado.

Para **Python**, a biblioteca `_adal_` precisará ser instalada.  Isso está disponível por meio de pip.

Verifique os [notebooks de exemplo](https://github.com/microsoft/sql-spark-connector/tree/master/samples) para obter exemplos.

## <a name="support"></a>Suporte

O Conector do Apache Spark para SQL do Azure e SQL Server é um projeto de software livre. Esse conector não vem com nenhum suporte da Microsoft. Para problemas com o ou perguntas sobre o conector, crie um problema neste repositório de projeto. A comunidade do conector está ativa e monitorando envios.

## <a name="next-steps"></a>Próximas etapas

Acesse o [repositório GitHub do conector do SQL Spark](https://github.com/microsoft/sql-spark-connector).

Para obter mais informações sobre os níveis de isolamento, confira [SET TRANSACTION ISOLATION LEVEL (Transact-SQL)](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md).