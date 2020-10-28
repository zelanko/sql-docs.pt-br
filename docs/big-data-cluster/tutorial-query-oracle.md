---
title: Consultar dados externos no Oracle
titleSuffix: SQL Server big data clusters
description: Este tutorial demonstra como consultar dados do Oracle de um cluster de Big Data do SQL Server 2019. Você cria uma tabela externa sobre os dados no Oracle e, em seguida, executa uma consulta.
author: MikeRayMSFT
ms.author: dacoelho
ms.reviewer: mikeray
ms.date: 10/01/2020
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 48d7fb0f41446fa54f1376a9a84f7dbff7017960
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92196080"
---
# <a name="tutorial-query-oracle-from-sql-server-big-data-cluster"></a>Tutorial: consultar o Oracle em um Cluster de Big Data do SQL Server

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

Este tutorial demonstra como consultar dados do Oracle de um cluster de Big Data do SQL Server 2019. Para executar este tutorial, você precisará ter acesso a um servidor Oracle. É necessária uma conta de usuário do Oracle com privilégios de leitura para o objeto externo. Há suporte para a autenticação de usuário de proxy do Oracle. Se você não tiver acesso, este tutorial poderá dar uma noção de como funciona a virtualização de dados para fontes de dados externos no cluster de Big Data do SQL Server.

Neste tutorial, você aprenderá como:

> [!div class="checklist"]
> * Criar uma tabela externa para dados em um banco de dados Oracle externo.
> * Unir esses dados com os dados de alto valor na instância mestre.

> [!TIP]
> Se preferir, você poderá baixar e executar um script para os comandos neste tutorial. Para obter instruções, confira os [Exemplos de virtualização de dados](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/data-virtualization) no GitHub.

## <a name="prerequisites"></a><a id="prereqs"></a> Pré-requisitos

- [Ferramentas de Big Data](deploy-big-data-tools.md)
   - **kubectl**
   - **Azure Data Studio**
   - **Extensão do SQL Server 2019**
- [Carregar dados de exemplo em seu cluster de Big Data](tutorial-load-sample-data.md)

## <a name="create-an-oracle-table"></a>Criar uma tabela do Oracle

As etapas a seguir criam uma tabela de exemplo chamada `INVENTORY` no Oracle.

1. Conecte-se a uma instância e banco de dados Oracle que você deseja usar para este tutorial.

1. Execute a seguinte instrução para criar a tabela `INVENTORY`:

   ```sql
    CREATE TABLE "INVENTORY"
    (
        "INV_DATE" NUMBER(10,0) NOT NULL,
        "INV_ITEM" NUMBER(10,0) NOT NULL,
        "INV_WAREHOUSE" NUMBER(10,0) NOT NULL,
        "INV_QUANTITY_ON_HAND" NUMBER(10,0)
    );

    CREATE INDEX INV_ITEM ON HR.INVENTORY(INV_ITEM);
    ```

1. Importe o conteúdo do arquivo **inventory.csv** para esta tabela. Esse arquivo foi criado pelos scripts de criação de exemplo na seção [Pré-requisitos](#prereqs).

## <a name="create-an-external-data-source"></a>Criar uma fonte de dados externos

A primeira etapa é criar uma fonte de dados externos que possa acessar seu servidor Oracle.

1. No Azure Data Studio, conecte-se à instância mestre do SQL Server do cluster de Big Data. Para obter mais informações, confira [Conectar-se à instância mestre do SQL Server](connect-to-big-data-cluster.md#master).

1. Clique duas vezes na conexão na janela **Servidores** para mostrar o painel do servidor da instância mestre do SQL Server. Selecione **Nova Consulta** .

   ![Consulta da instância mestre do SQL Server](./media/tutorial-query-oracle/sql-server-master-instance-query.png)

1. Execute o seguinte comando Transact-SQL para alterar o contexto para o banco de dados **Vendas** na instância mestre.

   ```sql
   USE Sales
   GO
   ```

1. Crie uma credencial no escopo do banco de dados para se conectar ao servidor Oracle. Forneça as credenciais apropriadas para o servidor Oracle na instrução a seguir.

   ```sql
   CREATE DATABASE SCOPED CREDENTIAL [OracleCredential]
   WITH IDENTITY = '<oracle_user,nvarchar(100),SYSTEM>', SECRET = '<oracle_user_password,nvarchar(100),manager>';
   ```

1. Crie uma fonte de dados externos que aponte para o servidor Oracle.

   ```sql
   CREATE EXTERNAL DATA SOURCE [OracleSalesSrvr]
   WITH (LOCATION = 'oracle://<oracle_server,nvarchar(100)>',CREDENTIAL = [OracleCredential]);
   ```

### <a name="optional-oracle-proxy-authentication"></a>Opcional: autenticação de proxy do Oracle

O Oracle dá suporte à autenticação de proxy para fornecer um controle de acesso refinado. Um usuário de proxy se conecta ao banco de dados Oracle usando suas credenciais e representa outro usuário no banco de dados. 

Um usuário de proxy pode ser configurado para ter acesso limitado em comparação com o usuário que está sendo representado. Por exemplo, um usuário de proxy pode ter permissão para se conectar usando uma função de banco de dados específica do usuário que está sendo representado. A identidade do usuário que está se conectando ao banco de dados do Oracle por meio do usuário de proxy é preservada na conexão, mesmo que vários usuários estejam se conectando por meio da autenticação de proxy. Isso permite que o Oracle imponha o controle de acesso e faça auditoria das ações executadas em nome do usuário real.

Caso seu cenário exija o uso de um usuário de proxy do Oracle, __substitua as etapas 4 e 5 anteriores pelas descritas a seguir__ .

4. Crie uma credencial no escopo do banco de dados para se conectar ao servidor Oracle. Forneça as credenciais de usuário de proxy do Oracle apropriadas para o servidor Oracle na instrução a seguir.

   ```sql
   CREATE DATABASE SCOPED CREDENTIAL [OracleProxyCredential]
   WITH IDENTITY = '<oracle_proxy_user,nvarchar(100),SYSTEM>', SECRET = '<oracle_proxy_user_password,nvarchar(100),manager>';
   ```

5. Crie uma fonte de dados externos que aponte para o servidor Oracle.

   ```sql
   CREATE EXTERNAL DATA SOURCE [OracleSalesSrvr]
   WITH (LOCATION = 'oracle://<oracle_server,nvarchar(100)>',
   CONNECTION_OPTIONS = 'ImpersonateUser=% CURRENT_USER',
   CREDENTIAL = [OracleProxyCredential]);
   ```

## <a name="create-an-external-table"></a>Criar uma tabela externa

Em seguida, crie uma tabela externa chamada **iventory_ora** sobre a tabela `INVENTORY` no servidor Oracle.

```sql
CREATE EXTERNAL TABLE [inventory_ora]
    ([inv_date] DECIMAL(10,0) NOT NULL, [inv_item] DECIMAL(10,0) NOT NULL,
    [inv_warehouse] DECIMAL(10,0) NOT NULL, [inv_quantity_on_hand] DECIMAL(10,0))
WITH (DATA_SOURCE=[OracleSalesSrvr],
        LOCATION='<oracle_service_name,nvarchar(30),xe>.<oracle_schema,nvarchar(128),HR>.<oracle_table,nvarchar(128),INVENTORY>');
```

> [!NOTE]
> Os nomes da tabela e de coluna usarão o identificador entre aspas do ANSI SQL ao consultar o Oracle. Como resultado, os nomes diferenciam maiúsculas de minúsculas. É importante especificar o nome na definição da tabela externa que corresponde ao caso exato dos nomes de tabela e coluna nos metadados do Oracle.

## <a name="query-the-data"></a>Consultar os dados

Execute a consulta a seguir para unir os dados na tabela externa `iventory_ora` com as tabelas no banco de dados `Sales` local.

```sql
SELECT TOP(100) w.w_warehouse_name, i.inv_item, SUM(i.inv_quantity_on_hand) as total_quantity
  FROM [inventory_ora] as i
  JOIN item as it
    ON it.i_item_sk = i.inv_item
  JOIN warehouse as w
    ON w.w_warehouse_sk = i.inv_warehouse
 WHERE it.i_category = 'Books' and i.inv_item BETWEEN 1 and 18000 --> get items within specific range
 GROUP BY w.w_warehouse_name, i.inv_item;
```

## <a name="clean-up"></a>Limpar

Use o comando a seguir para remover os objetos de banco de dados criados neste tutorial.

```sql
DROP EXTERNAL TABLE [inventory_ora];
DROP EXTERNAL DATA SOURCE [OracleSalesSrvr] ;
DROP DATABASE SCOPED CREDENTIAL [OracleCredential];
```

## <a name="next-steps"></a>Próximas etapas

Saiba como ingerir dados no pool de dados:
> [!div class="nextstepaction"]
> [Carregar dados no pool de dados](tutorial-data-pool-ingest-sql.md)
