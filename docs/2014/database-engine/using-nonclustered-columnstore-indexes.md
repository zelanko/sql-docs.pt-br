---
title: Usando índices Columnstore não clusterizado | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-indexes
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 4c341fb8-7cb1-4cab-921b-e80b751d6c19
caps.latest.revision: 7
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.openlocfilehash: fd711b644c551da7a658eff7ede74007d69a2286
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36013396"
---
# <a name="using-nonclustered-columnstore-indexes"></a>Usando índices columnstore não clusterizados
  Descreve as tarefas principais para usar um índice columnstore não clusterizado em uma tabela do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 Para obter uma visão geral de índices columnstore, consulte [Columnstore Indexes Described](../relational-databases/indexes/columnstore-indexes-described.md).  
  
 Para obter informações sobre índices columnstore clusterizados, consulte [Using Clustered Columnstore Indexes](../relational-databases/indexes/indexes.md).  
  
## <a name="contents"></a>Sumário  
  
-   [Criar um índice Columnstore não clusterizado](../../2014/database-engine/using-nonclustered-columnstore-indexes.md#load)  
  
-   [Alterar os dados em um índice Columnstore não clusterizado](../../2014/database-engine/using-nonclustered-columnstore-indexes.md#change)  
  
##  <a name="load"></a> Criar um índice Columnstore não clusterizado  
 Para carregar dados em um índice columnstore não clusterizado, primeiro carregue dados em uma tabela rowstore tradicional armazenada como um heap ou clusterizado de índice e, em seguida, usar [CREATE COLUMNSTORE INDEX &#40;Transact-SQL&#41; ](/sql/t-sql/statements/create-columnstore-index-transact-sql) para criar um índice ColumnStore.  
  
 ![Carregando dados em um índice columnstore](../../2014/database-engine/media/sql-server-pdw-columnstore-loadprocess-nonclustered.gif "carregar dados em um índice columnstore")  
  
##  <a name="change"></a> Alterar os dados em um índice Columnstore não clusterizado  
 Quando você cria um índice columnstore não clusterizado em uma tabela, não pode modificar diretamente os dados nessa tabela. Uma consulta com INSERT, UPDATE, DELETE ou MERGE falhará e retornará uma mensagem de erro. Para adicionar ou modificar os dados na tabela, siga um destes procedimentos:  
  
-   Desabilite o índice columnstore. Depois, você pode atualizar os dados na tabela. Se você desabilitar o índice columnstore, poderá recriar o índice columnstore quando concluir a atualização dos dados. Por exemplo:  
  
    ```  
    ALTER INDEX mycolumnstoreindex ON mytable DISABLE;  
    -- update mytable --  
    ALTER INDEX mycolumnstoreindex on mytable REBUILD  
    ```  
  
-   Descarte o índice columnstore, atualizar a tabela e, em seguida, recrie o índice de columnstore com CREATE COLUMNSTORE INDEX. Por exemplo:  
  
    ```  
    DROP INDEX mycolumnstoreindex ON mytable  
    -- update mytable --  
    CREATE NONCLUSTERED COLUMNSTORE INDEX mycolumnstoreindex ON mytable;  
  
    ```  
  
-   Carregar dados em uma tabela de preparação sem um índice columnstore. Criar um índice columnstore na tabela de preparo. Alternar a tabela de preparo para uma partição vazia da tabela principal.  
  
-   Alternar uma partição da tabela com o índice columnstore para uma tabela de preparo vazia. Se houver um índice columnstore na tabela de preparo, desabilite o índice columnstore. Executar quaisquer atualizações. Criar (ou recriar) o índice columnstore. Alternar a tabela de preparo para a partição anterior (não vazia) da tabela principal.  
  

  
  
