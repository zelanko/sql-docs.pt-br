---
title: Configurar o PolyBase para acessar dados externos no SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: polybase
ms.topic: conceptual
author: Abiola
ms.author: aboke
manager: craigg
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: d2b4bb2249f0c4a6ec57c037db54c490f3066e2b
ms.sourcegitcommit: 41979c9d511b3eeb45134d30ccb0dbc6bba70f1a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/01/2018
ms.locfileid: "50757941"
---
# <a name="configure-polybase-to-access-external-data-in-sql-server"></a>Configurar o PolyBase para acessar dados externos no SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo explica como usar o PolyBase em uma instância do SQL Server para consultar dados externos em outra instância do SQL Server.

## <a name="prerequisites"></a>Prerequisites

Se você ainda não instalou o PolyBase, veja [Instalação do PolyBase](polybase-installation.md). O artigo sobre a instalação explica os pré-requisitos.

## <a name="configure-an-external-table"></a>Configurar uma tabela externa

Para consultar os dados de uma fonte de dados do SQL Server, você precisa criar tabelas externas para fazer referência aos dados externos. Esta seção fornece código de exemplo para criar essas tabelas externas. 
 
Para obter um desempenho de consulta ideal, crie estatísticas em colunas de tabelas externas, especialmente aquelas usadas para junções, filtros e agregações.

Estes objetos serão criados nesta seção:

- CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL) 
- CREATE EXTERNAL DATA SOURCE (Transact-SQL) 
- CREATE EXTERNAL TABLE (Transact-SQL) 
- CREATE STATISTICS (Transact-SQL)

1. Crie uma chave mestra no banco de dados. Uma chave mestra é necessária para criptografar o segredo da credencial.

     ```sql
      CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo';  
     ```

1. Crie uma credencial com escopo de banco de dados.

     ```sql
     /*  specify credentials to external data source
     *  IDENTITY: user name for external source.  
     *  SECRET: password for external source.
     */
     CREATE DATABASE SCOPED CREDENTIAL SqlServerCredentials   
     WITH IDENTITY = 'username', Secret = 'password';
     ```

1. Crie uma fonte de dados externa, usando [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md). Especifique a localização da fonte de dados externa e as credenciais para a fonte de dados do SQL Server.

     ```sql
    /*  LOCATION: Location string should be of format '<vendor>://<server>[:<port>]'.
    *  PUSHDOWN: specify whether computation should be pushed down to the source. ON by default.
    *  CREDENTIAL: the database scoped credential, created above.
    */  
    CREATE EXTERNAL DATA SOURCE SQLServerInstance
    WITH ( 
    LOCATION = sqlserver://SqlServer,
    -- PUSHDOWN = ON | OFF,
      CREDENTIAL = SQLServerCredentials
    );

     ```

1. Crie esquemas para dados externos.

     ```sql
     CREATE SCHEMA sqlserver;
     GO
     ```

1.  Crie tabelas externas que representem os dados armazenados em uma instância do SQL Server externo com [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md).
 
     ```sql
     /*  LOCATION: sql server table/view in 'database_name.schema_name.object_name' format
     *  DATA_SOURCE: the external data source, created above.
     */
     CREATE EXTERNAL TABLE sqlserver.customer(
     C_CUSTKEY INT NOT NULL,
     C_NAME VARCHAR(25) NOT NULL,
     C_ADDRESS VARCHAR(40) NOT NULL,
     C_NATIONKEY INT NOT NULL,
     C_PHONE CHAR(15) NOT NULL,
     C_ACCTBAL DECIMAL(15,2) NOT NULL,
     C_MKTSEGMENT CHAR(10) NOT NULL,
     C_COMMENT VARCHAR(117) NOT NULL
      )
      WITH (
      LOCATION='tpch_10.dbo.customer',
      DATA_SOURCE=SqlServerInstance
     );
      ```

1. Crie estatísticas em uma tabela externa.

     ```sql
      CREATE STATISTICS CustomerCustKeyStatistics ON sqlserver.customer (C_CUSTKEY) WITH FULLSCAN; 
     ```

## <a name="sql-server-connector-compatible-types"></a>Tipos compatíveis com o conector do SQL Server

É possível fazer uma conexão com outras fontes de dados que reconhecem uma conexão do SQL Server. Use o conector do PolyBase do SQL Server para criar uma tabela externa do SQL Data Warehouse do Azure e do Banco de Dados SQL do Azure. Para realizar essa tarefa, siga as mesmas etapas listadas anteriormente. Verifique se o endereço do servidor, a porta, a cadeia de caracteres de localização e as credenciais no escopo do banco de dados estão correlacionados aos da fonte de dados compatível à qual você deseja se conectar.

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre o PolyBase, consulte [Visão geral do PolyBase do SQL Server](polybase-guide.md).
