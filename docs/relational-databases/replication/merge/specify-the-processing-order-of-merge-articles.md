---
title: Especificar a ordem de processamento dos artigos de mesclagem | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- articles [SQL Server replication], processing order
- merge replication [SQL Server replication], article processing order
ms.assetid: d151e2c5-cf50-4cb3-a829-8f32455dbd66
caps.latest.revision: "34"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a4476f6aaa996dff5ed88258a2cb9430a62774cd
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2018
---
# <a name="specify-the-processing-order-of-merge-articles"></a>Especificar a ordem de processamento dos artigos de mesclagem
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] em diante, é possível substituir a ordem padrão do processamento de artigos para publicações de mesclagem. Isso é útil, por exemplo, se você definir a integridade referencial por meio de gatilhos e esses gatilhos precisarem ser acionados em uma determinada ordem.  
  
 **Para especificar a ordem de processamento dos artigos**  
  
-   Programação de Transact-SQL de Replicação: [especificar a ordem de processamento de artigos da tabela de mesclagem &#40;Programação de Transact-SQL de Replicação&#41;](../../../relational-databases/replication/publish/specify-the-processing-order-of-merge-table-articles.md)  
  
## <a name="how-processing-order-is-determined"></a>Como a ordem de processamento é determinada  
 Durante a sincronização da mesclagem, os artigos são, por padrão, processados na ordem exigida pelas dependências entre objetos, incluindo as limitações de integridade referencial declarativa (DRI) definidas nas tabelas de base. O processamento envolve a enumeração das alterações em uma tabela e depois a aplicação dessas alterações. Se não houver DRI presente, mas existirem filtros de junção ou registros lógicos entre artigos de tabela, os artigos serão processados na ordem exigida pelos filtros e registros lógicos. Os artigos que não se relacionam a nenhum outro artigo por meio de DRI, filtros de junção, registros lógicos ou outras dependências serão processados segundo o apelido do artigo na tabela do sistema do [sysmergearticles &#40;Transact-SQL&#41;](../../../relational-databases/system-tables/sysmergearticles-transact-sql.md).  
  
 Considere uma publicação que inclua as tabelas **SalesOrderHeader** e **SalesOrderDetail** com uma coluna de chave primária **SalesOrderID** na tabela **SalesOrderHeader** e uma coluna de chave estrangeira correspondente **SalesOrderID** na tabela **SalesOrderDetail** . Durante a sincronização, a replicação de mesclagem impede violações de chave estrangeira ao inserir qualquer linha nova em **SalesOrderHeader** antes de inserir linhas associadas em **SalesOrderDetail**. Do mesmo modo, linhas são excluídas de **SalesOrderDetail** antes de a linha associada ser excluída de **SalesOrderHeader**.  
  
 Porém, em alguns aplicativos a integridade referencial é imposta por meio de gatilhos de banco de dados, ou no nível do aplicativo, e não por meio de DRI. Considerando a publicação descrita acima, em vez de DRI, a tabela **SalesOrderDetail** poderia ter um gatilho de inserção que garanta que a linha associada na tabela **SalesOrderHeader** existe antes de permitir uma inserção. **SalesOrderHeader** poderia ter um gatilho de exclusão que garante que não há nenhuma linha associada em **SalesOrderDetail** antes de permitir uma exclusão. A replicação de mesclagem não leva em conta os gatilhos ao determinar a ordem de processamento de artigos porque não pode determinar qual será o resultado do gatilho até que ele tenha sido acionado. Do mesmo modo, a replicação não pode levar em conta as restrições definidas no nível do aplicativo.  
  
 Quando a integridade referencial é mantida por meio de gatilhos ou no nível do aplicativo, você deve especificar a ordem em que os artigos devem ser processados. No exemplo com gatilhos, você especificaria que a tabela **SalesOrderHeader** deve ser processada antes de **SalesOrderDetail**, porque a ordem dos artigos é baseada na ordem de inserção. A replicação de mesclagem inverterá a ordem automaticamente para as exclusões. A replicação de mesclagem não apresentará falha sem a ordenação de artigos, porque o Merge Agent continua a processar os artigos se houver uma violação de restrição; depois do processamento de todos os outros artigos, ele tenta novamente as operações que apresentaram falha. Especificar a ordem de artigos simplesmente evita as novas tentativas e o processamento adicional associado a elas. Se você especificar uma ordem incorreta (por exemplo, uma que faça com que os registros detalhados sejam processados antes dos registros do cabeçalho), a replicação de mesclagem irá tentar o processamento repetidamente, até obter êxito.  
  
## <a name="see-also"></a>Consulte Também  
 [Opções de artigos para a replicação de mesclagem](../../../relational-databases/replication/merge/article-options-for-merge-replication.md)   
 [Agrupar alterações em linhas relacionadas com registros lógicos](../../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)   
 [Join Filters](../../../relational-databases/replication/merge/join-filters.md)  
  
  
