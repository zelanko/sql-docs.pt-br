---
title: "Especificar que as exclus&#245;es n&#227;o devem ser controladas para artigos de mesclagem (Programa&#231;&#227;o Transact-SQL de replica&#231;&#227;o) | Microsoft Docs"
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
  - "controle de exclusão condicional [replicação do SQL Server]"
  - "replicação de mesclagem [replicação do SQL Server], controle de exclusão condicional"
ms.assetid: 0fe330ca-5fb5-422e-ad6f-92fb5d6a3b6c
caps.latest.revision: 34
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Especificar que as exclus&#245;es n&#227;o devem ser controladas para artigos de mesclagem (Programa&#231;&#227;o Transact-SQL de replica&#231;&#227;o)
    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 Por padrão, a replicação de mesclagem sincroniza comandos DELETE entre o Publicador e o Assinante. A replicação de mesclagem permite que as linhas sejam retidas no banco de dados de assinatura mesmo após terem sido excluídas da publicação e vice-versa. Especifique de forma programática que os comandos DELETE sejam ignorados durante a criação de um novo artigo ou habilite essa funcionalidade posteriormente, usando procedimentos armazenados de replicação.  
  
> [!IMPORTANT]  
>  Habilitar essa funcionalidade resultará em não convergência, o que significa que os dados presentes no Assinante não refletirão dados no Publicador da forma correta. É preciso implementar um mecanismo próprio para remover manualmente as linhas excluídas.  
  
### Para especificar que as exclusões sejam ignoradas para um novo artigo de mesclagem  
  
1.  No publicador do banco de dados de publicação, execute [sp_addmergearticle & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md). Especifique um valor de **false** para **@delete_tracking**. Para obter mais informações, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
    > [!NOTE]  
    >  Se a tabela de origem para um artigo já estiver publicada em outra publicação, o valor de **delete_tracking** deve ser o mesmo para os dois artigos.  
  
### Para especificar que as exclusões sejam ignoradas para um artigo de mesclagem existente  
  
1.  Para determinar se a compensação de erros é habilitada para um artigo, execute [sp_helpmergearticle & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md) e observe o valor de **delete_tracking** no conjunto de resultados. Se esse valor for **0**, exclusões já estão sendo ignoradas.  
  
2.  Se o valor da etapa 1 for **1**, execute [sp_changemergearticle & #40. O Transact-SQL e 41;](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) o publicador do banco de dados de publicação. Especifique um valor de **delete_tracking** para **@property**, e um valor de **false** para **@value**.  
  
    > [!NOTE]  
    >  Se a tabela de origem para um artigo já estiver publicada em outra publicação, o valor de **delete_tracking** deve ser o mesmo para os dois artigos.  
  
## Consulte também  
 [Otimizar o desempenho da replicação de mesclagem com o controle de exclusão condicional](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-conditional-delete-tracking.md)  
  
  