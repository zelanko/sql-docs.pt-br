---
title: "Especificar que as exclusões não devem ser controladas para artigos de mesclagem | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- TSQL
helpviewer_keywords:
- conditional delete tracking [SQL Server replication]
- merge replication [SQL Server replication], conditional delete tracking
ms.assetid: 0fe330ca-5fb5-422e-ad6f-92fb5d6a3b6c
caps.latest.revision: 34
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 285e91369dfc5572b0da94fc110ce8b9e720b8a6
ms.lasthandoff: 04/11/2017

---
# <a name="specify-that-deletes-should-not-be-tracked-for-merge-articles"></a>Especificar que as exclusões não devem ser controladas para artigos de mesclagem
    
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 Por padrão, a replicação de mesclagem sincroniza comandos DELETE entre o Publicador e o Assinante. A replicação de mesclagem permite que as linhas sejam retidas no banco de dados de assinatura mesmo após terem sido excluídas da publicação e vice-versa. Especifique de forma programática que os comandos DELETE sejam ignorados durante a criação de um novo artigo ou habilite essa funcionalidade posteriormente, usando procedimentos armazenados de replicação.  
  
> [!IMPORTANT]  
>  Habilitar essa funcionalidade resultará em não convergência, o que significa que os dados presentes no Assinante não refletirão dados no Publicador da forma correta. É preciso implementar um mecanismo próprio para remover manualmente as linhas excluídas.  
  
### <a name="to-specify-that-deletes-be-ignored-for-a-new-merge-article"></a>Para especificar que as exclusões sejam ignoradas para um novo artigo de mesclagem  
  
1.  No Publicador no banco de dados de publicação, execute o [sp_addmergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md). Especifique um valor de **false** para **@delete_tracking**. Para obter mais informações, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
    > [!NOTE]  
    >  Se a tabela de fonte de um artigo já estiver publicada em outra publicação, o valor de **delete_tracking** deverá ser o mesmo de ambos os artigos.  
  
### <a name="to-specify-that-deletes-be-ignored-for-an-existing-merge-article"></a>Para especificar que as exclusões sejam ignoradas para um artigo de mesclagem existente  
  
1.  Para determinar se a compensação de erro está habilitada para um artigo, execute [sp_helpmergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md) e observe o valor de **delete_tracking** no conjunto de resultados. Se este valor for **0**, as exclusões já estão sendo ignoradas.  
  
2.  Se o valor da etapa 1 for **1**, execute [sp_changemergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) no Publicador do banco de dados de publicação. Especifique um valor de **delete_tracking** para **@property**, e um valor de **false** para **@value**.  
  
    > [!NOTE]  
    >  Se a tabela de fonte de um artigo já estiver publicada em outra publicação, o valor de **delete_tracking** deverá ser o mesmo de ambos os artigos.  
  
## <a name="see-also"></a>Consulte também  
 [Otimizar o desempenho da replicação de mesclagem com o controle de exclusão condicional](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-conditional-delete-tracking.md)  
  
  
