---
title: 'Acessar dados externos: Tipos genéricos ODBC – PolyBase'
description: O PolyBase no SQL Server permite que você se conecte a fontes de dados compatíveis usando o conector ODBC. Instalar o driver ODBC e criar tabelas externas.
ms.date: 02/19/2020
ms.custom: seo-lt-2019
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mikeray
monikerRange: '>= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions'
ms.openlocfilehash: 97cc801d15371255e56a0e6fd5904edf0d74e4ed
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85741047"
---
# <a name="configure-polybase-to-access-external-data-in-sql-server"></a>Configurar o PolyBase para acessar dados externos no SQL Server

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

O PolyBase no SQL Server 2019 permite que você se conecte a fontes de dados compatíveis com o ODBC usando o conector ODBC.

Este artigo fornece alguns exemplos usando um driver ODBC. Confira se há exemplos específicos com seu provedor ODBC. Veja a documentação do driver ODBC da fonte de dados para determinar as opções de cadeia de conexão apropriadas. Os exemplos neste artigo podem não se aplicar a nenhum driver ODBC específico.

## <a name="prerequisites"></a>Pré-requisitos

>[!NOTE]
>Este recurso requer o SQL Server no Windows.

* [Instalação do PolyBase](polybase-installation.md).

* Antes de criar um banco de dados de credencial no escopo, uma [Chave Mestra](../../t-sql/statements/create-master-key-transact-sql.md) deve ser criada.

## <a name="install-the-odbc-driver"></a>Instalar o driver ODBC

Primeiro, baixe e instale o driver ODBC da fonte de dados à qual você deseja se conectar em cada um dos nós do PolyBase. Depois que o driver estiver instalado corretamente, você poderá ver e testar o driver em **Administrador da Fonte de Dados ODBC**.

![Grupos de escala horizontal do PolyBase](../../relational-databases/polybase/media/polybase-odbc-admin.png) 

No exemplo acima, o nome do driver está circulado em vermelho. Use esse nome quando criar a fonte de dados externa.

> [!IMPORTANT]
> Para aprimorar o desempenho da consulta, habilite o pool de conexões. Isso pode ser feito em **Administrador da Fonte de Dados ODBC**.

## <a name="create-an-external-table"></a>Criar uma tabela externa

Para consultar os dados de uma fonte de dados ODBC, você precisa criar tabelas externas para referenciar os dados externos. Esta seção fornece um código de exemplo para criar tabelas externas.

Os seguintes comandos Transact-SQL são usados nesta seção:

* [CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)](../../t-sql/statements/create-database-scoped-credential-transact-sql.md)
* [CREATE EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md) 
* [CREATE STATISTICS (Transact-SQL)](../../t-sql/statements/create-statistics-transact-sql.md)

1. Crie uma credencial no escopo do banco de dados para acessar a fonte ODBC.

    ```sql
    CREATE DATABASE SCOPED CREDENTIAL <credential_name> WITH IDENTITY = '<username>', Secret = '<password>';
    ```

    Por exemplo, o exemplo a seguir cria uma credencial chamada `credential_name`, com uma identidade de `username` e uma senha complexa.

    ```sql
    CREATE DATABASE SCOPED CREDENTIAL credential_name WITH IDENTITY = 'username', Secret = 'BycA4ZjrE#*2W%!';
    ```

1. Crie uma fonte de dados externa, usando [CREATE EXTERNAL DATA SOURCE](../../t-sql/statements/create-external-data-source-transact-sql.md).

    ```sql
    CREATE EXTERNAL DATA SOURCE <external_data_source_name>
    WITH ( LOCATION = odbc://<ODBC server address>[:<port>],
    CONNECTION_OPTIONS = 'Driver={<Name of Installed Driver>};
    ServerNode = <name of server  address>:<Port>',
    -- PUSHDOWN = [ON] | OFF,
    CREDENTIAL = <credential_name> );
    ```

    O seguinte exemplo cria uma fonte de dados externa:
    * Chamada `external_data_source_name`
    * Localizada no `SERVERNAME` do ODBC e na porta `4444`
    * Conectando-se com `CData ODBC Driver For SAP 2015` – Este é o driver criado em [Instalar o driver ODBC](#install-the-odbc-driver)
    * No `ServerNode` `sap_server_node` porta `5555`
    * Configurada para processar a propagação para os níveis interiores do servidor (`PUSHDOWN = ON`)
    * Usar a credencial `credential_name`

    ```sql
    CREATE EXTERNAL DATA SOURCE external_data_source_name
    WITH ( LOCATION = odbc://SERVERNAME:4444,
    CONNECTION_OPTIONS = 'Driver={CData ODBC Driver For SAP 2015};
    ServerNode = sap_server_node:5555',
    PUSHDOWN = ON,
    CREDENTIAL = credential_name );
    ```

1. **Opcional:** Crie estatísticas em uma tabela externa.

    Para obter desempenho de consulta ideal, é recomendável criar estatísticas em colunas de tabelas externas, especialmente aquelas usadas para junções, filtros e agregações.

    ```sql
    CREATE STATISTICS statistics_name ON customer (C_CUSTKEY) WITH FULLSCAN; 
    ```

>[!IMPORTANT]
>Após criar uma fonte de dados externa, use o comando [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md) para criar uma tabela que possa ser consultada por essa fonte.

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre o PolyBase, consulte [Visão geral do PolyBase do SQL Server](polybase-guide.md).
