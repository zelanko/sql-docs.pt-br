---
title: "Especificar o n&#237;vel de rastreamento e resolu&#231;&#227;o de conflitos para artigos de mesclagem | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "resolução de conflitos de replicação de mesclagem [replicação do SQL Server], níveis"
  - "artigos [replicação do SQL Server], resolução de conflitos"
  - "resolução de conflitos [replicação do SQL Server], replicação de mesclagem"
ms.assetid: 81e9ecb6-1d31-4a78-b32a-96f7f4d67077
caps.latest.revision: 35
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 35
---
# Especificar o n&#237;vel de rastreamento e resolu&#231;&#227;o de conflitos para artigos de mesclagem
  Este tópico descreve como especificar o nível de rastreamento e resolução de conflitos para artigos de mesclagem no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 Quando uma assinatura em uma publicação de mesclagem é sincronizada, a replicação verifica os conflitos causados pelas alterações nos mesmos dados feitos no Publicador e no Assinante. Especifique se os conflitos serão detectados no nível da linha, onde todas as alterações de linha são consideradas conflito, ou no nível da coluna, onde apenas as alterações da mesma linha e da coluna são consideradas conflito. A resolução de conflitos para artigos é realizada no nível da linha. Para obter mais informações sobre a detecção e a resolução de conflitos quando registros lógicos são usados, consulte [Detecting and Resolving Conflicts in Logical Records](../../../relational-databases/replication/merge/detecting-and-resolving-conflicts-in-logical-records.md).  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
-   **Para especificar o nível de rastreamento e resolução de conflitos para artigos de mesclagem, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   Se você alterar o nível de controle depois de inicializadas as assinaturas, essas assinaturas deverão ser reinicializadas. Para obter mais informações sobre os efeitos de alterações de propriedade, consulte [alterar propriedades da publicação e artigo](../../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
-   Com controle em nível de linha e de coluna, a resolução de conflito é sempre feita em nível de linha: a linha vencedora substitui a perdedora. A replicação de mesclagem também permite especificar que os conflitos sejam rastreados e resolvidos em nível de registro lógico, mas essas opções não estão disponíveis no [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]. Para obter informações sobre como definir estas opções de procedimentos armazenados de replicação, consulte [Define a Logical Record Relationship Between Merge Table Articles](../../../relational-databases/replication/publish/define-a-logical-record-relationship-between-merge-table-articles.md).  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Especificar coluna-nível de linha ou de rastreamento para artigos de mesclagem no **propriedades** Guia do **Propriedades do artigo** caixa de diálogo, que está disponível no Assistente de nova publicação e o **Propriedades de publicação - \< publicação>** caixa de diálogo. Para obter mais informações sobre como usar o assistente e acessar a caixa de diálogo, consulte [criar uma publicação](../../../relational-databases/replication/publish/create-a-publication.md) e [Exibir e modificar propriedades de publicação](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### Para especificar controle em nível de linha ou de coluna  
  
1.  Sobre o **artigos** página do Assistente de nova publicação ou o **Propriedades de publicação - \< publicação>** caixa de diálogo, selecione uma tabela.  
  
2.  Clique em **Propriedades de Artigos**e então clique em **Definir Propriedades do Artigo Realçado da Tabela** ou **Definir Propriedades de Todos os Artigos da Tabela**.  
  
3.  No **propriedades** Guia do **Propriedades do artigo \< artigo>** caixa de diálogo, selecione um dos seguintes valores para o **nível de rastreamento** propriedade: **controle em nível de linha** ou **controle em nível de coluna**.  
  
4.  Se você estiver no **Propriedades de publicação - \< publicação>** caixa de diálogo, clique em **OK** para salvar e fechar a caixa de diálogo.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
  
#### Para especificar as opções de controle de conflito para um novo artigo de mesclagem  
  
1.  No publicador do banco de dados de publicação, execute [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) e especificar um dos valores a seguir para **@column_tracking**:  
  
    -   **True** -usar o controle de nível de coluna para o artigo.  
  
    -   **False** -rastreamento de nível de linha de uso, que é o padrão.  
  
#### Para alterar as opções de rastreamento de conflito para um novo artigo de mesclagem  
  
1.  Para determinar o opções de controle para um artigo de mesclagem de conflito, execute [sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md). Observe o valor da **column_tracking** opção no conjunto de resultados para o artigo. Um valor de **1** significa que o controle de nível de coluna está sendo usado e um valor de **0** significa que o controle de nível de linha está sendo usado.  
  
2.  No publicador do banco de dados de publicação, execute [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md). Especifique um valor de **column_tracking** para **@property** e um dos seguintes valores para **@value**:  
  
    -   **True** -usar o controle de nível de coluna para o artigo.  
  
    -   **False** -rastreamento de nível de linha de uso, que é o padrão.  
  
     Especifique um valor de **1** para ambos **@force_invalidate_snapshot** e **@force_reinit_subscription**.  
  
## Consulte também  
 [Detecção e resolução de conflito de replicação de mesclagem avançada ](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [Detectando e resolvendo conflitos em registros lógicos](../../../relational-databases/replication/merge/detecting-and-resolving-conflicts-in-logical-records.md)   
 [Definir uma relação de registro lógico entre artigos da tabela de mesclagem](../../../relational-databases/replication/publish/define-a-logical-record-relationship-between-merge-table-articles.md)   
 [Detectar e resolver conflitos de replicação de mesclagem](../../../relational-databases/replication/merge/detect-and-resolve-merge-replication-conflicts.md)  
  
  