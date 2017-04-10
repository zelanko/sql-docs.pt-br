---
title: "Adicionar e descartar artigos em uma publica&#231;&#227;o (SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "artigos [replicação do SQL Server], descartando"
  - "excluindo artigos"
  - "descartando artigos"
  - "adicionando artigos"
  - "artigos [replicação do SQL Server], adicionando"
ms.assetid: d5a3e536-62d2-4473-a178-877ba52f7d7f
caps.latest.revision: 35
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 35
---
# Adicionar e descartar artigos em uma publica&#231;&#227;o (SQL Server Management Studio)
  Inicialmente, adicione os artigos a uma publicação ao criá-la no Assistente para Nova Publicação. Para obter mais informações sobre como usar esse assistente, consulte [criar uma publicação](../../../relational-databases/replication/publish/create-a-publication.md).  
  
 Depois de uma publicação é criada, adicionar e excluir artigos sobre o **artigos** página do **Propriedades de publicação - \< publicação>** caixa de diálogo. Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md). Para obter informações sobre as considerações para adicionar e descartar artigos, consulte [Adicionar e descartar artigos de publicações existentes](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md).  
  
### Para adicionar um artigo após a criação de uma publicação  
  
1.  No **artigos** página do **Propriedades de publicação - \< publicação>** caixa de diálogo, desmarque o **Mostrar somente os objetos na lista marcados** caixa de seleção. Isso permitirá ver os objetos não publicados, no banco de dados de publicação.  
  
2.  Marque a caixa de seleção próxima a cada artigo que você quer adicionar.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### Para excluir um artigo  
  
1.  Sobre o **artigos** página do **Propriedades de publicação - \< publicação>** caixa de diálogo, desmarque a caixa de seleção ao lado de cada artigo que deseja excluir.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## Consulte também  
 [Defina um Artigo](../../../relational-databases/replication/publish/define-an-article.md)   
 [Publicar dados e objetos de banco de dados](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  