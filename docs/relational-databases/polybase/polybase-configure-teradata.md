---
title: Configurar o PolyBase para acessar dados externos no Teradata | Microsoft Docs
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
ms.openlocfilehash: 7abd9873b3aeefb5644ade0497fe89c47d7cd343
ms.sourcegitcommit: 41979c9d511b3eeb45134d30ccb0dbc6bba70f1a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/01/2018
ms.locfileid: "50757951"
---
# <a name="configure-polybase-to-access-external-data-in-teradata"></a>Configurar o PolyBase para acessar dados externos no Teradata

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Esse artigo explica como usar o PolyBase em uma instância do SQL Server para consultar dados externos no Teradata.

## <a name="prerequisites"></a>Prerequisites

Se você ainda não instalou o PolyBase, veja [Instalação do PolyBase](polybase-installation.md). O artigo sobre a instalação explica os pré-requisitos.

Para usar o PolyBase no Teradata, o VC++ redistribuível é necessário.
 
## <a name="configure-an-external-table"></a>Configurar uma tabela externa

Para consultar os dados de uma fonte de dados do Teradata, você precisa criar tabelas externas para fazer referência aos dados externos. Esta seção fornece código de exemplo para criar essas tabelas externas. 

Estes objetos serão criados nesta seção:

- CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)
- CREATE EXTERNAL DATA SOURCE (Transact-SQL) 
- CREATE EXTERNAL TABLE (Transact-SQL) 
- CREATE STATISTICS (Transact-SQL)

1. Crie uma chave mestra no banco de dados, caso ela ainda não exista. Uma chave mestra é necessária para criptografar o segredo da credencial.

     ```sql
      CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';  
     ```
    **Argumentos**

    PASSWORD ='password'

    É a senha usada para criptografar a chave mestra no banco de dados? A senha precisa atender aos requisitos da política de senha do Windows do computador que hospeda a instância do SQL Server.

1. Crie uma credencial com escopo de banco de dados.
 
     ```sql
     /*  specify credentials to external data source
      *  IDENTITY: user name for external source.  
     *  SECRET: password for external source.
     */
     CREATE DATABASE SCOPED CREDENTIAL credential_name
     WITH IDENTITY = 'username', Secret = 'password'
     ```

1. Crie uma fonte de dados externa, usando [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md).

     ```sql
    /*  LOCATION: Location string should be of format '<vendor>://<server>[:<port>]'.
    *  PUSHDOWN: specify whether computation should be pushed down to the source. ON by default.
    * CONNECTION_OPTIONS: Specify driver location
    *  CREDENTIAL: the database scoped credential, created above.
    */  
    CREATE EXTERNAL DATA SOURCE external_data_source_name
    WITH ( 
    LOCATION = teradata://<server address>[:<port>],
   -- PUSHDOWN = ON | OFF,
    CREDENTIAL =credential_name
    );

     ```

1.  Crie tabelas externas que representam dados armazenados em um sistema Teradata externo com [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md).
 
     ```sql
     /*  LOCATION: Teradata table/view in '<database_name>.<object_name>' format
      *  DATA_SOURCE: the external data source, created above.
      */
     CREATE EXTERNAL TABLE customer(
      L_ORDERKEY INT NOT NULL,
      L_PARTKEY INT NOT NULL,
     L_SUPPKEY INT NOT NULL,
     L_LINENUMBER INT NOT NULL,
     L_QUANTITY DECIMAL(15,2) NOT NULL,
     L_EXTENDEDPRICE DECIMAL(15,2) NOT NULL,
     L_DISCOUNT DECIMAL(15,2) NOT NULL,
     L_TAX DECIMAL(15,2) NOT NULL,
     L_RETURNFLAG CHAR NOT NULL,
     L_LINESTATUS CHAR NOT NULL,
     L_SHIPDATE DATE NOT NULL,
     L_COMMITDATE DATE NOT NULL,
     L_RECEIPTDATE DATE NOT NULL,
     L_SHIPINSTRUCT CHAR(25) NOT NULL,
     L_SHIPMODE CHAR(10) NOT NULL,
     L_COMMENT VARCHAR(44) NOT NULL
     )
     WITH (
     LOCATION='customer',
     DATA_SOURCE= external_data_source_name
     );
     ```

1. *Opcional:* criar estatísticas em uma tabela externa.

    Para obter um desempenho de consulta ideal, crie estatísticas em colunas de tabelas externas, especialmente aquelas usadas para junções, filtros e agregações.

     ```sql
      CREATE STATISTICS statistics_name ON customer (C_CUSTKEY) WITH FULLSCAN; 
     ```

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre o PolyBase, consulte [Visão geral do PolyBase do SQL Server](polybase-guide.md).
