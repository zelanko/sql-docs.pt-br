---
title: "Especificar o nível de rastreamento e resolução de conflitos para artigos de mesclagem | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], levels
- articles [SQL Server replication], conflict resolution
- conflict resolution [SQL Server replication], merge replication
ms.assetid: 81e9ecb6-1d31-4a78-b32a-96f7f4d67077
caps.latest.revision: 35
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 18b5650ce77b40deb101a16ebd1379600394dcbf
ms.lasthandoff: 04/11/2017

---
# <a name="specify-the-conflict-tracking-and-resolution-level-for-merge-articles"></a>Especificar o nível de rastreamento e resolução de conflitos para artigos de mesclagem
  Este tópico descreve como especificar o nível de rastreamento e resolução de conflitos para artigos de mesclagem no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 Quando uma assinatura em uma publicação de mesclagem é sincronizada, a replicação verifica os conflitos causados pelas alterações nos mesmos dados feitos no Publicador e no Assinante. Especifique se os conflitos serão detectados no nível da linha, onde todas as alterações de linha são consideradas conflito, ou no nível da coluna, onde apenas as alterações da mesma linha e da coluna são consideradas conflito. A resolução de conflitos para artigos é realizada no nível da linha. Para obter mais informações sobre a detecção e a resolução de conflitos quando registros lógicos são usados, consulte [Detecting and Resolving Conflicts in Logical Records](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-resolving-in-logical-record.md).  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
-   **Para especificar o nível de rastreamento e resolução de conflitos para artigos de mesclagem, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   Se você alterar o nível de controle depois de inicializadas as assinaturas, essas assinaturas deverão ser reinicializadas. Para obter mais informações sobre os efeitos das alterações de propriedades, consulte [Alterar propriedades da publicação e do artigo](../../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
-   Com controle em nível de linha e de coluna, a resolução de conflito é sempre feita em nível de linha: a linha vencedora substitui a perdedora. A replicação de mesclagem também permite especificar que os conflitos sejam rastreados e resolvidos em nível de registro lógico, mas essas opções não estão disponíveis no [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]. Para obter informações sobre como definir estas opções de procedimentos armazenados de replicação, consulte [Define a Logical Record Relationship Between Merge Table Articles](../../../relational-databases/replication/publish/define-a-logical-record-relationship-between-merge-table-articles.md).  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Especifique o nível de linha ou coluna de rastreamento para mesclar artigos na guia **Propriedades** da caixa de diálogo **Propriedades do artigo**, que está disponível no Assistente para Nova Publicação e a caixa de diálogo **Propriedades da Publicação – \<Publicação>**. Para obter mais informações sobre como usar o assistente e acessar a caixa de diálogo, consulte [Criar uma publicação](../../../relational-databases/replication/publish/create-a-publication.md) e [Exibir e modificar as propriedades da publicação](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### <a name="to-specify-row--or-column-level-tracking"></a>Para especificar controle em nível de linha ou de coluna  
  
1.  Na página **Artigos** do Assistente para Nova Publicação ou na caixa de diálogo **Propriedades de Publicação – \<Publicação>**, selecione uma tabela.  
  
2.  Clique em **Propriedades de Artigos**e então clique em **Definir Propriedades do Artigo Realçado da Tabela** ou **Definir Propriedades de Todos os Artigos da Tabela**.  
  
3.  Na guia **Propriedades** da caixa de diálogo **Propriedade do Artigo \<Artigo>**, selecione um dos seguintes valores para a propriedade **Nível de rastreamento**: **Rastreamento em nível de linha** ou **Rastreamento em nível de coluna**.  
  
4.  Se você estiver na caixa de diálogo **Propriedades da Publicação – \<Publicação>**, clique em **OK** para salvar e fechar a caixa de diálogo.  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
  
#### <a name="to-specify-conflict-tracking-options-for-a-new-merge-article"></a>Para especificar as opções de controle de conflito para um novo artigo de mesclagem  
  
1.  No Publicador do banco de dados de publicação, execute [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) e especifique um dos seguintes valores para **@column_tracking**:  
  
    -   **true** - Use controle no nível da coluna para o artigo.  
  
    -   **false** - Use controle no nível da linha, que é o padrão.  
  
#### <a name="to-change-conflict-tracking-options-for-a-merge-article"></a>Para alterar as opções de rastreamento de conflito para um novo artigo de mesclagem  
  
1.  Para determinar as opções de rastreamento de conflito para um artigo de mesclagem, execute [sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md). Observe o valor da opção **column_tracking** no conjunto de resultados do artigo. Um valor de **1** significa que o controle no nível da coluna está em uso, e o valor de **0** significa que o controle no nível da linha está em uso.  
  
2.  No Publicador do banco de dados de publicação, execute [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md). Especifique um valor de **column_tracking** para **@property** e um dos valores a seguir para **@value**:  
  
    -   **true** - Use controle no nível da coluna para o artigo.  
  
    -   **false** - Use controle no nível da linha, que é o padrão.  
  
     Especifique um valor de **1** para ambos **@force_invalidate_snapshot** e **@force_reinit_subscription**.  
  
## <a name="see-also"></a>Consulte também  
 [Advanced Merge Replication Conflict Detection and Resolution](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [Detecting and Resolving Conflicts in Logical Records](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-resolving-in-logical-record.md)   
 [Define a Logical Record Relationship Between Merge Table Articles](../../../relational-databases/replication/publish/define-a-logical-record-relationship-between-merge-table-articles.md)   
 [Detectar e resolver conflitos de replicação de mesclagem](../../../relational-databases/replication/merge/advanced-merge-replication-resolve-merge-replication-conflicts.md)  
  
  
