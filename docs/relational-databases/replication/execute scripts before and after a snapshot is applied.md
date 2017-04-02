---
title: "Executar scripts antes e depois de um instant&#226;neo ser aplicado (SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "12/29/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "instantâneos [replicação do SQL Server], scripts"
  - "scripts [replicação do SQL Server], instantâneos"
  - "replicação de instantâneo [SQL Server], scripts"
ms.assetid: b7bb1e4c-5b48-4bb1-9dc8-47c911f2cc82
caps.latest.revision: 39
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Executar scripts antes e depois de um instant&#226;neo ser aplicado (SQL Server Management Studio)
  Especifique um script opcional para executar antes ou depois que o instantâneo é aplicado a **instantâneo** página do **Propriedades de publicação - \< publicação>** caixa de diálogo. Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
> [!NOTE]  
>  Essas opções não estarão disponíveis se o **formato do instantâneo** opção é definida como **caracteres**.  
  
### Para executar um script antes ou depois de um instantâneo ser aplicado  
  
1.  Sobre o **instantâneo** página do **Propriedades de publicação - \< publicação>** caixa de diálogo:  
  
    -   Para especificar um script para executar antes que o instantâneo é aplicado, clique em **Procurar** para navegar para o script ou insira um caminho para o script de **antes de aplicar o instantâneo, executar este script** caixa de texto.  
  
        > [!NOTE]  
        >  O Agente de Distribuição ou Agente de Mesclagem devem ter permissões de leitura para o diretório especificado. Se forem usadas assinaturas pull, você deve especificar um diretório compartilhado como um caminho universal naming convention (UNC), como \\\computername\scripts\myscript.sql.  
  
    -   Para especificar um script a ser executado após o instantâneo é aplicado, clique em **Procurar** para navegar para o script ou insira um caminho UNC para o script no **após a aplicação do instantâneo, executar este script** caixa de texto.  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## Consulte também  
 [Configurar propriedades de instantâneo e 40; Programação Transact-SQL de replicação e 41;](../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)   
 [Alterar propriedades da publicação e do artigo](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [Executar scripts antes e depois da aplicação do instantâneo](../../relational-databases/replication/execute-scripts-before-and-after-the-snapshot-is-applied.md)   
 [Inicializar uma assinatura com um instantâneo](../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
  
  