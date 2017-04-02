---
title: "Especificar a ordem de processamento de artigos da tabela de mesclagem (Programa&#231;&#227;o Transact-SQL de replica&#231;&#227;o) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "artigos [replicação do SQL Server], ordem de processamento"
  - "replicação de mesclagem [replicação do SQL Server], artigo sobre ordem de processamento"
ms.assetid: 9fe576a2-f5fb-4fdf-bd7d-cb322021b669
caps.latest.revision: 33
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Especificar a ordem de processamento de artigos da tabela de mesclagem (Programa&#231;&#227;o Transact-SQL de replica&#231;&#227;o)
  A replicação de mesclagem permite que você especifique a ordem em que artigos são processados pelo Agente de Mesclagem durante o processo de sincronização. Você pode atribuir uma ordem a cada artigo programaticamente ao criar um artigo usando procedimentos armazenados de replicação. Os artigos são processados em ordem crescente de valores. Se dois artigos tiverem o mesmo valor, serão processados simultaneamente. Para obter mais informações, consulte [especificar o processamento de ordem de mesclar artigos](../../../relational-databases/replication/merge/specify-the-processing-order-of-merge-articles.md).  
  
### Para especificar a ordem de processamento de um novo artigo de mesclagem  
  
1.  No publicador do banco de dados de publicação, execute [sp_addmergearticle & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md). Especifique um valor inteiro que representa a ordem de processamento para o artigo para **@processing_order**. Para obter mais informações, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
    > [!NOTE]  
    >  Ao criar artigos ordenados, você deverá deixar intervalos entre os valores de ordem de artigo. Isto facilitará a definição de novos valores no futuro. Por exemplo, se você tiver três artigos para a qual você precisa especificar uma ordem de processamento fixa, defina o valor de **@processing_order** para 10, 20 e 30 em vez de 1, 2 e 3, respectivamente.  
  
### Para alterar a ordem de processamento de um artigo de mesclagem  
  
1.  Para determinar a ordem de processamento de um artigo, execute [sp_helpmergearticle & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md) e observe o valor de **processing_order** no conjunto de resultados.  
  
2.  No publicador do banco de dados de publicação, execute [sp_changemergearticle & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md). Especifique um valor de **processing_order** para **@property** e um valor inteiro que representa a ordem de processamento de **@value**.  
  
## Consulte também  
 [Especificar a ordem de processamento dos artigos de mesclagem](../../../relational-databases/replication/merge/specify-the-processing-order-of-merge-articles.md)  
  
  