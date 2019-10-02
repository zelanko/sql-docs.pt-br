---
title: Consultar dados externos no Oracle
titleSuffix: SQL Server big data clusters
description: Este tutorial demonstra como consultar dados Oracle de um [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]. Você cria uma tabela externa sobre os dados no Oracle e, em seguida, executa uma consulta.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: ''
ms.date: 08/21/2019
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: b880e3758481e5b061221bd2753b5a26f01ed856
ms.sourcegitcommit: 8732161f26a93de3aa1fb13495e8a6a71519c155
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71708362"
---
# <a name="tutorial-query-oracle-from-a-sql-server-big-data-cluster"></a>Tutorial: Consultar o Oracle em um cluster de Big Data do SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este tutorial demonstra como consultar dados do Oracle de um cluster de Big Data do SQL Server 2019. Para executar este tutorial, você precisará ter acesso a um servidor Oracle. Se você não tiver acesso, este tutorial poderá dar uma noção de como funciona a virtualização de dados para fontes de dados externos no cluster de Big Data do SQL Server.

Neste tutorial, você aprenderá a:

> [!div class="checklist"]
> * Criar uma tabela externa para dados em um banco de dados Oracle externo.
> * Unir esses dados com os dados de alto valor na instância mestre.

> [!TIP]
> Se preferir, você poderá baixar e executar um script para os comandos neste tutorial. Para obter instruções, confira os [Exemplos de virtualização de dados](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/data-virtualization) no GitHub.

## <a id="prereqs"></a> Pré-requisitos

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

1. Clique duas vezes na conexão na janela **Servidores** para mostrar o painel do servidor da instância mestre do SQL Server. Selecione **Nova Consulta**.

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
