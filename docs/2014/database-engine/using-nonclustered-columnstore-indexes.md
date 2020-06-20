---
title: Usando índices Columnstore não clusterizados | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: 4c341fb8-7cb1-4cab-921b-e80b751d6c19
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: c876eb6fdd466349ac369dcff8e292bc0839c669
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84927767"
---
# <a name="using-nonclustered-columnstore-indexes"></a>Usando índices columnstore não clusterizados
  Descreve as tarefas principais para usar um índice columnstore não clusterizado em uma tabela do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .

 Para obter uma visão geral de índices columnstore, consulte [Columnstore Indexes Described](../relational-databases/indexes/columnstore-indexes-described.md).

 Para obter informações sobre índices columnstore clusterizados, consulte [Using Clustered Columnstore Indexes](../relational-databases/indexes/indexes.md).

## <a name="contents"></a>Sumário

-   [Criar um índice columnstore não clusterizado](../../2014/database-engine/using-nonclustered-columnstore-indexes.md#load)

-   [Alterar os dados em um índice columnstore não clusterizado](../../2014/database-engine/using-nonclustered-columnstore-indexes.md#change)

##  <a name="create-a-nonclustered-columnstore-index"></a><a name="load"></a>Criar um índice Columnstore não clusterizado
 Para carregar dados em um índice columnstore não clusterizado, primeiro carregue os dados em uma tabela de armazenamento tradicional armazenada como um índice de heap ou cluster e, em seguida, use [Create COLUMNSTORE index &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-columnstore-index-transact-sql) para criar um índice columnstore.

 ![Carregando dados em um índice columnstore](../../2014/database-engine/media/sql-server-pdw-columnstore-loadprocess-nonclustered.gif "Carregando dados em um índice columnstore")

##  <a name="change-the-data-in-a-nonclustered-columnstore-index"></a><a name="change"></a>Alterar os dados em um índice Columnstore não clusterizado
 Quando você cria um índice columnstore não clusterizado em uma tabela, não pode modificar diretamente os dados nessa tabela. Uma consulta com INSERT, UPDATE, DELETE ou MERGE falhará e retornará uma mensagem de erro. Para adicionar ou modificar os dados na tabela, siga um destes procedimentos:

-   Desabilite o índice columnstore. Depois, você pode atualizar os dados na tabela. Se você desabilitar o índice columnstore, poderá recriar o índice columnstore quando concluir a atualização dos dados. Por exemplo:

    ```
    ALTER INDEX mycolumnstoreindex ON mytable DISABLE;
    -- update mytable --
    ALTER INDEX mycolumnstoreindex on mytable REBUILD
    ```

-   Descarte o índice columnstore, atualize a tabela e crie novamente o índice columnstore com CREATE COLUMNSTORE INDEX. Por exemplo:

    ```
    DROP INDEX mycolumnstoreindex ON mytable
    -- update mytable --
    CREATE NONCLUSTERED COLUMNSTORE INDEX mycolumnstoreindex ON mytable;

    ```

-   Carregar dados em uma tabela de preparação sem um índice columnstore. Criar um índice columnstore na tabela de preparo. Alternar a tabela de preparo para uma partição vazia da tabela principal.

-   Alternar uma partição da tabela com o índice columnstore para uma tabela de preparo vazia. Se houver um índice columnstore na tabela de preparo, desabilite o índice columnstore. Executar quaisquer atualizações. Criar (ou recriar) o índice columnstore. Alternar a tabela de preparo para a partição anterior (não vazia) da tabela principal.




