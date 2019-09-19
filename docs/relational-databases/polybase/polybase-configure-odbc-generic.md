---
title: Configurar o PolyBase para acessar dados externos com tipos genéricos ODBC | Microsoft Docs
ms.date: 04/23/2019
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
author: Abiola
ms.author: aboke
ms.reviewer: mikeray
monikerRange: '>= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions'
ms.openlocfilehash: b07d97563406a464bfdb38dba7b3aa1d51e27c34
ms.sourcegitcommit: f76b4e96c03ce78d94520e898faa9170463fdf4f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70874782"
---
# <a name="configure-polybase-to-access-external-data-in-sql-server"></a>Configurar o PolyBase para acessar dados externos no SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

O PolyBase no SQL Server 2019 permite que você se conecte a fontes de dados compatíveis com o ODBC usando o conector ODBC. 

## <a name="prerequisites"></a>Prerequisites

Observação: o recurso só funciona no SQL Server no Windows. 

Se você ainda não instalou o PolyBase, veja [Instalação do PolyBase](polybase-installation.md).

 Antes de criar um banco de dados de credencial no escopo, uma [Chave Mestra](../../t-sql/statements/create-master-key-transact-sql.md) deve ser criada. 

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

Os seguintes comandos Transact-SQL são usados nesta seção:

- [CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)
- [CREATE EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md) 
- [CREATE STATISTICS (Transact-SQL)](../../t-sql/statements/create-statistics-transact-sql.md)

1. Crie uma credencial no escopo do banco de dados para acessar a fonte ODBC.

    ```sql
    /*  specify credentials to external data source
    *  IDENTITY: user name for external source. 
    *  SECRET: password for external source.
    */
    CREATE DATABASE SCOPED CREDENTIAL credential_name WITH IDENTITY = 'username', Secret = 'password';
    ```

1. Crie uma fonte de dados externa, usando [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md).

    ```sql
    /*  LOCATION: Location string should be of format '<type>://<server>[:<port>]'.
    *  PUSHDOWN: specify whether computation should be pushed down to the source. ON by default.
    *CONNECTION_OPTIONS: Specify driver location
    *  CREDENTIAL: the database scoped credential, created above.
    */  
    CREATE EXTERNAL DATA SOURCE external_data_source_name
    WITH ( LOCATION = odbc://<ODBC server address>[:<port>],
    CONNECTION_OPTIONS = 'Driver={<Name of Installed Driver>};
    ServerNode = <name of server  address>:<Port>',
    -- PUSHDOWN = ON | OFF,
    CREDENTIAL = credential_nam );
    ```

1. **Opcional:** Crie estatísticas em uma tabela externa.

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

Para obter desempenho de consulta ideal, é recomendável criar estatísticas em colunas de tabelas externas, especialmente aquelas usadas para junções, filtros e agregações.

    ```sql
    CREATE STATISTICS statistics_name ON customer (C_CUSTKEY) WITH FULLSCAN; 
    ```

>[!IMPORTANT] 
>Depois de criar uma fonte de dados externa, você pode usar o comando [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md) para criar uma tabela que possa ser consultada por essa fonte. 

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre o PolyBase, consulte [Visão geral do PolyBase do SQL Server](polybase-guide.md).
