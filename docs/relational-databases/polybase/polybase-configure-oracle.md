---
title: Configurar o PolyBase para acessar dados externos no Oracle | Microsoft Docs
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
ms.openlocfilehash: 2b6fc4d849a964aa2a3f761e5d566e78f130d4a9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47748034"
---
# <a name="configure-polybase-to-access-external-data-in-oracle"></a>Configurar o PolyBase para acessar dados externos no Oracle

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

O artigo explica como usar o PolyBase em uma instância do SQL Server para consultar dados externos no Oracle.

## <a name="prerequisites"></a>Prerequisites

Se você ainda não instalou o PolyBase, veja [Instalação do PolyBase](polybase-installation.md). O artigo sobre a instalação explica os pré-requisitos.

## <a name="configure-an-external-table"></a>Configurar uma tabela externa

Para consultar os dados de uma fonte de dados do Oracle, você precisa criar tabelas externas para fazer referência aos dados externos. Esta seção fornece código de exemplo para criar essas tabelas externas. 
 
É recomendável criar estatísticas em colunas de tabelas externas, especialmente aquelas usadas para junções, filtros e agregações, a fim de ter o desempenho de consulta ideal.

Estes objetos serão criados nesta seção:

- CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL) 
- CREATE EXTERNAL DATA SOURCE (Transact-SQL) 
- CREATE EXTERNAL FILE FORMAT (Transact-SQL) 
- CREATE EXTERNAL TABLE (Transact-SQL) 
- CREATE STATISTICS (Transact-SQL)


1. Crie uma chave mestra no banco de dados. Isso é necessário para criptografar o segredo da credencial.

     ```sql
      CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0me!nfo';  
     ```

1. Crie uma credencial com escopo de banco de dados.

     ```sql
     /*  specify credentials to external data source
     *  IDENTITY: user name for external source.  
     *  SECRET: password for external source.
     */
      CREATE DATABASE SCOPED CREDENTIAL OracleCredentials 
     WITH IDENTITY = 'username', Secret = 'password';
     ```

1. Crie uma fonte de dados externa, usando [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md). Especifique o local da fonte de dados externa e credenciais para a fonte de dados do Oracle.

     ```sql
     /*  LOCATION: Server DNS name or IP address.
      *  PUSHDOWN: specify whether computation should be pushed down to the source. ON by default.
     *  CREDENTIAL: the database scoped credential, created above.
     */  
     CREATE EXTERNAL DATA SOURCE OracleInstance
     WITH ( 
     LOCATION = '<vendor>://<server>[:<port>]',
     -- PUSHDOWN = ON | OFF,
      CREDENTIAL = OracleCredentials
     );
     ```

1. Crie esquemas para dados externos
 
     ```sql
     CREATE SCHEMA oracle;
     GO
     ```

1.  Crie tabelas externas que representam dados armazenados no sistema [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md) do Oracle externo.
 
      ```sql
      /*  LOCATION: Oracle table/view in '<database_name>.<schema_name>.<object_name>' format
     *  DATA_SOURCE: the external data source, created above.
     */
      CREATE EXTERNAL TABLE oracle.orders(
      [O_ORDERKEY] DECIMAL(38) NOT NULL,
     [O_CUSTKEY] DECIMAL(38) NOT NULL,
     [O_ORDERSTATUS] CHAR COLLATE Latin1_General_BIN NOT NULL,
     [O_TOTALPRICE] DECIMAL(15,2) NOT NULL,
     [O_ORDERDATE] DATETIME2(0) NOT NULL,
     [O_ORDERPRIORITY] CHAR(15) COLLATE Latin1_General_BIN NOT NULL,
     [O_CLERK] CHAR(15) COLLATE Latin1_General_BIN NOT NULL,
     [O_SHIPPRIORITY] DECIMAL(38) NOT NULL,
     [O_COMMENT] VARCHAR(79) COLLATE Latin1_General_BIN NOT NULL
     )
     WITH (
      LOCATION='TPCH..ORDERS',
      DATA_SOURCE=OracleInstance
     );
     ```

1. Crie estatísticas em uma tabela externa para otimizar o desempenho.

     ```sql
      CREATE STATISTICS OrdersOrderKeyStatistics ON oracle.orders(O_ORDERKEY) WITH FULLSCAN;
     ```

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre o PolyBase, consulte [Visão geral do PolyBase do SQL Server](polybase-guide.md).
