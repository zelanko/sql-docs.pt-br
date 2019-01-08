---
title: Especificar a ordem de processamento de artigos de tabela de mesclagem (programação Transact-SQL de replicação) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- articles [SQL Server replication], processing order
- merge replication [SQL Server replication], article processing order
ms.assetid: 9fe576a2-f5fb-4fdf-bd7d-cb322021b669
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: fbc61994e251063fe6d23450582d44c77616a662
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52795568"
---
# <a name="specify-the-processing-order-of-merge-table-articles-replication-transact-sql-programming"></a>Especificar a ordem de processamento de artigos da tabela de mesclagem (Programação Transact-SQL de replicação)
  A replicação de mesclagem permite que você especifique a ordem em que artigos são processados pelo Agente de Mesclagem durante o processo de sincronização. Você pode atribuir uma ordem a cada artigo programaticamente ao criar um artigo usando procedimentos armazenados de replicação. Os artigos são processados em ordem crescente de valores. Se dois artigos tiverem o mesmo valor, serão processados simultaneamente. Para obter mais informações, consulte [Especificar a ordem de processamento dos artigos de mesclagem](../merge/specify-the-processing-order-of-merge-articles.md).  
  
### <a name="to-specify-the-processing-order-for-a-new-merge-article"></a>Para especificar a ordem de processamento de um novo artigo de mesclagem  
  
1.  No Publicador no banco de dados de publicação, execute o [sp_addmergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql). Especifique um valor inteiro que representa a ordem de processamento do artigo para **@processing_order**. Para obter mais informações, consulte [Define an Article](define-an-article.md).  
  
    > [!NOTE]  
    >  Ao criar artigos ordenados, você deverá deixar intervalos entre os valores de ordem de artigo. Isto facilitará a definição de novos valores no futuro. Por exemplo, se você tiver três artigos para os quais terá que especificar uma ordem de processamento fixa, defina o valor do **@processing_order** como 10, 20 e 30 em vez de 1, 2 e 3, respectivamente.  
  
### <a name="to-change-the-processing-order-of-a-merge-article"></a>Para alterar a ordem de processamento de um artigo de mesclagem  
  
1.  Para determinar a ordem de processamento de um artigo, execute [sp_helpmergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql) e observe o valor de **processing_order** no conjunto de resultados.  
  
2.  No Publicador no banco de dados de publicação, execute [sp_changemergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql). Especifique um valor de **processing_order** para **@property** e um valor inteiro que representa a ordem de processamento para **@value**.  
  
## <a name="see-also"></a>Consulte também  
 [Especificar a ordem de processamento dos artigos de mesclagem](../merge/specify-the-processing-order-of-merge-articles.md)  
  
  
