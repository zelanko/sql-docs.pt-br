---
title: Exibir informações sobre conflitos para publicações de mesclagem | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], viewing conflicts
- sp_helpmergeconflictrows
- viewing conflict information
- conflict resolution [SQL Server replication], merge replication
- sp_helpmergearticleconflicts
ms.assetid: 4907fe35-10ee-4f81-b924-fc419b1864d2
caps.latest.revision: 22
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a87f0391580dd8f577abf94997fd1448ae5bf198
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="view-conflict-information-for-merge-publications"></a>Exibir informações sobre conflitos para publicações de mesclagem
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Quando um conflito é resolvido em uma replicação de mesclagem, os dados da linha perdedora são gravados em uma tabela de conflitos. Os dados de conflito podem ser visualizados de forma programática, usando procedimentos armazenados de replicação. Para obter mais informações, consulte [Advanced Merge Replication Conflict Detection and Resolution](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md).  
  
### <a name="to-view-conflict-information-and-losing-row-data-for-all-types-of-conflicts"></a>Para visualizar informações sobre conflitos e dados de linhas perdedoras para todos os tipos de conflitos  
  
1.  No Publicador do banco de dados de publicação, execute [sp_helpmergepublication](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md). Observe os valores das colunas a seguir no conjunto de resultados.  
  
    -   **centralized_conflicts** - 1 indica que as linhas de conflito são armazenadas no Publicador, e 0 indica que as linhas de conflito não são armazenadas no Publicador.  
  
    -   **decentralized_conflicts** - 1 indica que as linhas de conflito são armazenadas no Assinante e 0 indica que as linhas de conflito não são armazenadas no Assinante.  
  
        > [!NOTE]  
        >  O comportamento do log de conflito de uma publicação de mesclagem é definido, usando-se o parâmetro **@conflict_logging** de [sp_addmergepublication](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md). O uso do parâmetro **@centralized_conflicts** não está mais em uso.  
  
     A tabela seguinte descreve os valores dessas colunas com base no valor especificado para **@conflict_logging**.  
  
    |@conflict_logging valor|centralized_conflicts|decentralized_conflicts|  
    |------------------------------|----------------------------|------------------------------|  
    |**Publicador**|1|0|  
    |**Assinante**|0|1|  
    |**ambos**|1|1|  
  
2.  No Publicador do banco de dados de publicação ou no Assinante, no banco de dados da assinatura, execute [sp_helpmergearticleconflicts](../../relational-databases/system-stored-procedures/sp-helpmergearticleconflicts-transact-sql.md). Especifique um valor para **@publication** para retornar apenas as informações de conflitos para artigos que pertençam a uma publicação específica. Isso retorna informações da tabela de conflitos para artigos com conflitos. Observe o valor de **conflict_table** para qualquer artigo de interesse. Se o valor de **conflict_table** para um artigo for NULL, só exclua conflitos que tenham ocorrido neste artigo.  
  
3.  (Opcional) Revise linhas de conflito para artigos de interesse. Dependendo dos valores de **centralized_conflicts** e **decentralized_conflicts** de etapa 1, execute um dos seguintes procedimentos:  
  
    -   No Publicador do banco de dados de publicação, execute [sp_helpmergeconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergeconflictrows-transact-sql.md). Especifique uma tabela de conflitos para o artigo (de etapa 1) para **@conflict_table**. (Opcional) Especifique um valor de **@publication** para restringir informações sobre conflitos retornadas a uma publicação específica. Isso retorna dados de linha e outra informações para a linha perdedora.  
  
    -   No Assinante, no banco de dados da assinatura, execute [sp_helpmergeconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergeconflictrows-transact-sql.md). Especifique uma tabela de conflitos para o artigo (de etapa 1) para **@conflict_table**. Isso retorna dados de linha e outra informações para a linha perdedora.  
  
### <a name="to-view-information-only-on-conflicts-where-the-delete-failed"></a>Para visualizar informações somente sobre conflitos onde a exclusão falhou  
  
1.  No Publicador do banco de dados de publicação, execute [sp_helpmergepublication](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md). Observe os valores das colunas a seguir no conjunto de resultados.  
  
    -   **centralized_conflicts** - 1 indica que as linhas de conflito são armazenadas no Publicador, e 0 indica que as linhas de conflito não são armazenadas no Publicador.  
  
    -   **decentralized_conflicts** - 1 indica que as linhas de conflito são armazenadas no Assinante e 0 indica que as linhas de conflito não são armazenadas no Assinante.  
  
        > [!NOTE]  
        >  O comportamento do log de conflito de uma publicação de mesclagem é definido usando-se o parâmetro **@conflict_logging** de [sp_addmergepublication](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md). O uso do parâmetro **@centralized_conflicts** não está mais em uso.  
  
2.  No Publicador do banco de dados de publicação ou no Assinante, no banco de dados da assinatura, execute [sp_helpmergearticleconflicts](../../relational-databases/system-stored-procedures/sp-helpmergearticleconflicts-transact-sql.md). Especifique um valor para **@publication** para retornar apenas as informações das tabelas de conflitos para artigos que pertençam a uma publicação específica. Isso retorna informações da tabela de conflitos para artigos com conflitos. Observe o valor de **source_object** para qualquer artigo de interesse. Se o valor de **conflict_table** para um artigo for NULL, só exclua conflitos que tenham ocorrido neste artigo.  
  
3.  (Opcional) Revise informações sobre conflitos para excluir conflitos. Dependendo dos valores de **centralized_conflicts** e **decentralized_conflicts** de etapa 1, execute um dos seguintes procedimentos:  
  
    -   No Publicador do banco de dados de publicação, execute [sp_helpmergedeleteconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergedeleteconflictrows-transact-sql.md). Especifique o nome da tabela de fonte (da etapa 1) na qual o conflito aconteceu para **@source_object**. (Opcional) Especifique um valor de **@publication** para restringir informações sobre conflitos retornadas a uma publicação específica. Isso retorna informações sobre conflitos de exclusão armazenadas no Publicador.  
  
    -   No Assinante, no banco de dados da assinatura, execute [sp_helpmergedeleteconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergedeleteconflictrows-transact-sql.md). Especifique o nome da tabela de fonte (da etapa 1) na qual o conflito aconteceu para **@source_object**. (Opcional) Especifique um valor de **@publication** para restringir informações sobre conflitos retornadas a uma publicação específica. Isso retorna informações sobre conflitos de exclusão armazenadas no Assinante.  
  
## <a name="see-also"></a>Consulte Também  
 [Advanced Merge Replication Conflict Detection and Resolution](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)  
  
  
