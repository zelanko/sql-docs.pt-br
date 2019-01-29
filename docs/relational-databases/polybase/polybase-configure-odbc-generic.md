---
title: Configurar o PolyBase para acessar dados externos com tipos genéricos ODBC | Microsoft Docs
ms.custom: ''
ms.date: 10/16/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: polybase
ms.topic: conceptual
author: Abiola
ms.author: aboke
manager: craigg
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 3cb5efcb4c4abdc29aa71bf4a5e59ebe039d8a9e
ms.sourcegitcommit: ee76381cfb1c16e0a063315c9c7005f10e98cfe6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2019
ms.locfileid: "55072841"
---
# <a name="configure-polybase-to-access-external-data-in-sql-server"></a>Configurar o PolyBase para acessar dados externos no SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

O PolyBase no SQL Server 2019 permite que você se conecte a fontes de dados compatíveis com o ODBC usando o conector ODBC. 

## <a name="prerequisites"></a>Prerequisites

Observação: o recurso só funciona no SQL Server no Windows. 

Se você ainda não instalou o PolyBase, veja [Instalação do PolyBase](polybase-installation.md).

Primeiro baixe e instale o driver ODBC da fonte de dados à qual você deseja se conectar em cada um dos nós do PolyBase. Depois que o driver estiver instalado corretamente, você poderá exibir e testar o driver em "Administrador da Fonte de Dados ODBC".

![Grupos de escala horizontal do PolyBase](../../relational-databases/polybase/media/polybase-odbc-admin.png) 

> **IMPORTANTE:**
> 
> Para melhorar o desempenho da consulta verifique se o pooling de conexão do driver está habilitado. Isso pode ser feito em "Administrador da Fonte de Dados ODBC".
> 
> **Observação**
> 
> O nome do driver (exemplo circulado acima) precisará ser especificado quando a fonte de dados externa for criada (Etapa 3 abaixo).

## <a name="create-an-external-table"></a>Criar uma tabela externa

Para consultar os dados de uma fonte de dados ODBC, você precisa criar tabelas externas para referenciar os dados externos. Esta seção fornece um código de exemplo para criar tabelas externas.

Estes objetos serão criados nesta seção:

- CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL) 
- CREATE EXTERNAL DATA SOURCE (Transact-SQL) 
- CREATE EXTERNAL TABLE (Transact-SQL) 
- CREATE STATISTICS (Transact-SQL)

1. Crie uma chave mestra no banco de dados, caso ainda não exista. Isso é necessário para criptografar o segredo da credencial.

     ```sql
      CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';  
     ```
    ## <a name="arguments"></a>Argumentos
    PASSWORD ='password'

    É a senha usada para criptografar a chave mestra no banco de dados. password precisa atender aos requisitos da política de senha do Windows do computador que está hospedando a instância do SQL Server.

1. Crie uma credencial no escopo do banco de dados para acessar a fonte de dados ODBC.

     ```sql
     /*  specify credentials to external data source
     *  IDENTITY: user name for external source.  
     *  SECRET: password for external source.
     */
     CREATE DATABASE SCOPED CREDENTIAL credential_name
     WITH IDENTITY = 'username', Secret = 'password';
     ```

1. Crie uma fonte de dados externa, usando [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md).

     ```sql
    /*  LOCATION: Location string should be of format '<type>://<server>[:<port>]'.
    *  PUSHDOWN: specify whether computation should be pushed down to the source. ON by default.
    *CONNECTION_OPTIONS: Specify driver location
    *  CREDENTIAL: the database scoped credential, created above.
    */  
    CREATE EXTERNAL DATA SOURCE external_data_source_name
    WITH ( 
    LOCATION = odbc://<ODBC server address>[:<port>],
    CONNECTION_OPTIONS = 'Driver={<Name of Installed Driver>};
    ServerNode = <name of server  address>:<Port>',
    -- PUSHDOWN = ON | OFF,
      CREDENTIAL = credential_name
    );

     ```


1.  Crie tabelas externas que representem dados na fonte de dados externa usando [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md).
 
     ```sql
     /*  LOCATION: ODBC data source table/view
     *  DATA_SOURCE: the external data source, created above.
     */
     CREATE EXTERNAL TABLE customer(
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
      LOCATION='customer',
      DATA_SOURCE= external_data_source_name
     );
      ```

1. **Opcional:** Crie estatísticas em uma tabela externa.

    É recomendável criar estatísticas em colunas de tabelas externas, especialmente aquelas usadas para junções, filtros e agregações, a fim de ter o desempenho de consulta ideal.

     ```sql
      CREATE STATISTICS statistics_name ON customer (C_CUSTKEY) WITH FULLSCAN; 
     ```

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre o PolyBase, consulte [Visão geral do PolyBase do SQL Server](polybase-guide.md).
