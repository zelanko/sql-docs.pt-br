---
title: 'Acessar dados externos: SQL Server – PolyBase'
description: Saiba como usar o PolyBase em uma instância do SQL Server para consultar dados externos em outra instância do SQL Server. Criar tabelas externas para fazer referência a dados externos.
ms.date: 10/06/2020
ms.custom: seo-lt-2019
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mikeray
monikerRange: '>= sql-server-linux-ver15 || >= sql-server-ver15'
ms.openlocfilehash: b03aa87cd92bd1aadbbb96a4019c76f3062dfb99
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97469127"
---
# <a name="configure-polybase-to-access-external-data-in-sql-server"></a>Configurar o PolyBase para acessar dados externos no SQL Server

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Este artigo explica como usar o PolyBase em uma instância do SQL Server para consultar dados externos em outra instância do SQL Server.

## <a name="prerequisites"></a>Pré-requisitos

Se você ainda não instalou o PolyBase, veja [Instalação do PolyBase](polybase-installation.md). O artigo sobre a instalação explica os pré-requisitos. Uma vez instalado, certifique-se também de [habilitar o PolyBase](polybase-installation.md#enable).

A fonte de dados externa do SQL Server usa a Autenticação SQL.

Antes de criar um banco de dados de credencial no escopo, uma [chave mestra](../../t-sql/statements/create-master-key-transact-sql.md) deve ser criada. 

## <a name="configure-a-sql-server-external-data-source"></a>Configurar uma fonte de dados externa do SQL Server

Para consultar os dados de uma fonte de dados do SQL Server, você precisa criar tabelas externas para fazer referência aos dados externos. Esta seção fornece código de exemplo para criar essas tabelas externas.
 
Para obter um desempenho de consulta ideal, crie estatísticas em colunas de tabelas externas, especialmente aquelas usadas para junções, filtros e agregações.

Os seguintes comandos Transact-SQL são usados nesta seção:

- [CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)
- [CREATE EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md) 
- [CREATE STATISTICS (Transact-SQL)](../../t-sql/statements/create-statistics-transact-sql.md)

1. Crie uma credencial no escopo do banco de dados para acessar a fonte do SQL Server. O exemplo a seguir cria uma credencial para a fonte de dados externa com `IDENTITY = 'username'` e `SECRET = 'password'`.

    ```sql
    CREATE DATABASE SCOPED CREDENTIAL SqlServerCredentials
    WITH IDENTITY = 'username', SECRET = 'password';
    ```
   >[!IMPORTANT]
   >O Conector ODBC do SQL para PolyBase dá suporte apenas à autenticação Básica, não à autenticação Kerberos.

1. Crie uma fonte de dados externa, usando [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md). O exemplo a seguir:

   - Cria uma fonte de dados externa nomeada como `SQLServerInstance`.
   - Identifica a fonte de dados externa (`LOCATION = '<vendor>://<server>[:<port>]'`). No exemplo, ele aponta para uma instância padrão do SQL Server.
   - Identifica se a computação deve ser enviada por push para a origem (`PUSHDOWN`). `PUSHDOWN` é `ON` por padrão.

   Por fim, o exemplo usa a credencial criada anteriormente.

    ```sql
    CREATE EXTERNAL DATA SOURCE SQLServerInstance
        WITH ( LOCATION = 'sqlserver://SqlServer',
        PUSHDOWN = ON,
        CREDENTIAL = SQLServerCredentials);
    ```

1. Opcionalmente, crie estatísticas em uma tabela externa.

  Para obter um desempenho de consulta ideal, crie estatísticas em colunas de tabelas externas, especialmente aquelas usadas para junções, filtros e agregações.

  ```sql
    CREATE STATISTICS statistics_name ON customer (C_CUSTKEY)
    WITH FULLSCAN;
  ```

>[!IMPORTANT]
>Depois de criar uma fonte de dados externa, você pode usar o comando [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md) para criar uma tabela que possa ser consultada por essa fonte.

## <a name="sql-server-connector-compatible-types"></a>Tipos compatíveis com o conector do SQL Server

É possível fazer uma conexão com outras fontes de dados que reconhecem uma conexão do SQL Server. Use o conector do PolyBase do SQL Server para criar uma tabela externa do Azure Synapse Analytics e do Banco de Dados SQL do Azure. Para realizar essa tarefa, siga as mesmas etapas listadas anteriormente. Verifique se o endereço do servidor, a porta, a cadeia de caracteres de localização e as credenciais no escopo do banco de dados estão correlacionados aos da fonte de dados compatível à qual você deseja se conectar.

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre o PolyBase, consulte [Visão geral do PolyBase do SQL Server](polybase-guide.md).
