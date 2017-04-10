---
title: "Exibir informa&#231;&#245;es sobre conflitos para publica&#231;&#245;es de mesclagem (Programa&#231;&#227;o Transact-SQL de replica&#231;&#227;o) | Microsoft Docs"
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
  - "resolução de conflitos de replicação de mesclagem [replicação do SQL Server], visualizando conflitos"
  - "sp_helpmergeconflictrows"
  - "visualizando informações de conflito"
  - "resolução de conflitos [replicação do SQL Server], replicação de mesclagem"
  - "sp_helpmergearticleconflicts"
ms.assetid: 4907fe35-10ee-4f81-b924-fc419b1864d2
caps.latest.revision: 22
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Exibir informa&#231;&#245;es sobre conflitos para publica&#231;&#245;es de mesclagem (Programa&#231;&#227;o Transact-SQL de replica&#231;&#227;o)
  Quando um conflito é resolvido em uma replicação de mesclagem, os dados da linha perdedora são gravados em uma tabela de conflitos. Os dados de conflito podem ser visualizados de forma programática, usando procedimentos armazenados de replicação. Para obter mais informações, consulte [Advanced Merge Replication Conflict Detection and Resolution](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md).  
  
### Para visualizar informações sobre conflitos e dados de linhas perdedoras para todos os tipos de conflitos  
  
1.  No publicador do banco de dados de publicação, execute [sp_helpmergepublication](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md). Observe os valores das colunas a seguir no conjunto de resultados.  
  
    -   **centralized_conflicts** -1 indica que as linhas de conflito são armazenadas no publicador e 0 indica que as linhas de conflito não são armazenadas no publicador.  
  
    -   **decentralized_conflicts** -1 indica que as linhas de conflito são armazenadas no assinante e 0 indica que as linhas de conflito não são armazenadas no assinante.  
  
        > [!NOTE]  
        >  O comportamento do log de conflito de uma publicação de mesclagem é definido usando o **@conflict_logging** parâmetro [sp_addmergepublication](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md). Usar o **@centralized_conflicts** parâmetro foi preterido.  
  
     A tabela a seguir descreve os valores dessas colunas com base no valor especificado para **@conflict_logging**.  
  
    |@conflict_logging value|centralized_conflicts|decentralized_conflicts|  
    |------------------------------|----------------------------|------------------------------|  
    |**publisher**|1|0|  
    |**subscriber**|0|1|  
    |**both**|1|1|  
  
2.  No Editor do banco de dados de publicação ou no assinante no banco de dados de assinatura, execute [sp_helpmergearticleconflicts](../../relational-databases/system-stored-procedures/sp-helpmergearticleconflicts-transact-sql.md). Especifique um valor para **@publication** para retornar apenas as informações de conflito para artigos que pertencem a uma publicação específica. Isso retorna informações da tabela de conflitos para artigos com conflitos. Observe o valor de **conflict_table** para todos os artigos de interesse. Se o valor de **conflict_table** para um artigo for NULL, só exclua conflitos ocorreram neste artigo.  
  
3.  (Opcional) Revise linhas de conflito para artigos de interesse. Dependendo dos valores de **centralized_conflicts** e **decentralized_conflicts** da etapa 1, faça o seguinte:  
  
    -   No publicador do banco de dados de publicação, execute [sp_helpmergeconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergeconflictrows-transact-sql.md). Especifique uma tabela de conflito para o artigo (obtido na etapa 1) para **@conflict_table**. (Opcional) Especifique um valor de **@publication** para restringir informações sobre conflitos retornadas a uma publicação específica. Isso retorna dados de linha e outra informações para a linha perdedora.  
  
    -   No assinante no banco de dados de assinatura, execute [sp_helpmergeconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergeconflictrows-transact-sql.md). Especifique uma tabela de conflito para o artigo (obtido na etapa 1) para **@conflict_table**. Isso retorna dados de linha e outra informações para a linha perdedora.  
  
### Para visualizar informações somente sobre conflitos onde a exclusão falhou  
  
1.  No publicador do banco de dados de publicação, execute [sp_helpmergepublication](../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md). Observe os valores das colunas a seguir no conjunto de resultados.  
  
    -   **centralized_conflicts** -1 indica que as linhas de conflito são armazenadas no publicador e 0 indica que as linhas de conflito não são armazenadas no publicador.  
  
    -   **decentralized_conflicts** -1 indica que as linhas de conflito são armazenadas no assinante e 0 indica que as linhas de conflito não são armazenadas no assinante.  
  
        > [!NOTE]  
        >  O comportamento do log de conflito de uma publicação de mesclagem é definido usando o **@conflict_logging** parâmetro [sp_addmergepublication](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md). Usar o **@centralized_conflicts** parâmetro foi preterido.  
  
2.  No Editor do banco de dados de publicação ou no assinante no banco de dados de assinatura, execute [sp_helpmergearticleconflicts](../../relational-databases/system-stored-procedures/sp-helpmergearticleconflicts-transact-sql.md). Especifique um valor para **@publication** para retornar apenas as informações da tabela de conflitos para artigos que pertencem a uma publicação específica. Isso retorna informações da tabela de conflitos para artigos com conflitos. Observe o valor de **source_object** para todos os artigos de interesse. Se o valor de **conflict_table** para um artigo for NULL, só exclua conflitos ocorreram neste artigo.  
  
3.  (Opcional) Revise informações sobre conflitos para excluir conflitos. Dependendo dos valores de **centralized_conflicts** e **decentralized_conflicts** da etapa 1, faça o seguinte:  
  
    -   No publicador do banco de dados de publicação, execute [sp_helpmergedeleteconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergedeleteconflictrows-transact-sql.md). Especifique o nome da tabela de origem (obtido na etapa 1) no qual o conflito ocorreu para **@source_object**. (Opcional) Especifique um valor de **@publication** para restringir informações sobre conflitos retornadas a uma publicação específica. Isso retorna informações sobre conflitos de exclusão armazenadas no Publicador.  
  
    -   No assinante no banco de dados de assinatura, execute [sp_helpmergedeleteconflictrows](../../relational-databases/system-stored-procedures/sp-helpmergedeleteconflictrows-transact-sql.md). Especifique o nome da tabela de origem (obtido na etapa 1) no qual o conflito ocorreu para **@source_object**. (Opcional) Especifique um valor de **@publication** para restringir informações sobre conflitos retornadas a uma publicação específica. Isso retorna informações sobre conflitos de exclusão armazenadas no Assinante.  
  
## Consulte também  
 [Detecção e resolução de conflito de replicação de mesclagem avançada ](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)  
  
  