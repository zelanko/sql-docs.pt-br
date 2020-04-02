---
title: 'Acessar dados externos: Teradata – PolyBase'
description: Saiba como usar o PolyBase em uma instância do SQL Server para consultar dados externos no Teradata. Criar tabelas externas para fazer referência aos dados externos.
ms.date: 12/13/2019
ms.custom: seo-lt-2019
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mikeray
monikerRange: '>= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions'
ms.openlocfilehash: a15cd01067c42c027bb327ef39d928978666abd3
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "80216011"
---
# <a name="configure-polybase-to-access-external-data-in-teradata"></a>Configurar o PolyBase para acessar dados externos no Teradata

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Esse artigo explica como usar o PolyBase em uma instância do SQL Server para consultar dados externos no Teradata.

## <a name="prerequisites"></a>Pré-requisitos

Se você ainda não instalou o PolyBase, veja [Instalação do PolyBase](polybase-installation.md). O artigo sobre a instalação explica os pré-requisitos.

Antes de criar um banco de dados de credencial no escopo, uma [chave mestra](../../t-sql/statements/create-master-key-transact-sql.md) deve ser criada. 

Para usar o PolyBase no Teradata, o VC++ redistribuível é necessário.
 
## <a name="configure-a-teradata-external-data-source"></a>Configurar uma fonte de dados externa do Teradata

Para consultar os dados de uma fonte de dados do Teradata, você precisa criar tabelas externas para fazer referência aos dados externos. Esta seção fornece código de exemplo para criar essas tabelas externas. 



Os seguintes comandos Transact-SQL são usados nesta seção:

- [CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)
- [CREATE EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md) 
- [CREATE STATISTICS (Transact-SQL)](../../t-sql/statements/create-statistics-transact-sql.md)

1. Crie uma credencial no escopo do banco de dados para acessar a origem do MongoDB.

    ```sql
    /*  specify credentials to external data source
    *  IDENTITY: user name for external source. 
    *  SECRET: password for external source.
    */
    CREATE DATABASE SCOPED CREDENTIAL credential_name WITH IDENTITY = 'username', Secret = 'password';
    ```

1. Crie uma fonte de dados externa, usando [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md).

    ```sql
    /*  LOCATION: Location string should be of format '<vendor>://<server>[:<port>]'.
    *  PUSHDOWN: specify whether computation should be pushed down to the source. ON by default.
    * CONNECTION_OPTIONS: Specify driver location
    *  CREDENTIAL: the database scoped credential, created above.
    */  
    CREATE EXTERNAL DATA SOURCE external_data_source_name
    WITH (LOCATION = teradata://<server address>[:<port>],
    -- PUSHDOWN = ON | OFF,
    CREDENTIAL =credential_name);
    ```

1. **Opcional:** Crie estatísticas em uma tabela externa.

    É recomendável criar estatísticas em colunas de tabelas externas, especialmente aquelas usadas para junções, filtros e agregações, a fim de ter o desempenho de consulta ideal.

    ```sql
    CREATE STATISTICS statistics_name ON customer (C_CUSTKEY) WITH FULLSCAN; 
    ```

>[!IMPORTANT] 
>Depois de criar uma fonte de dados externa, você pode usar o comando [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md) para criar uma tabela que possa ser consultada por essa fonte.

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre o PolyBase, consulte [Visão geral do PolyBase do SQL Server](polybase-guide.md).
