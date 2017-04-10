---
title: "Alternar entre modos de atualiza&#231;&#227;o para uma assinatura transacional atualiz&#225;vel | Microsoft Docs"
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
  - "replicação transacional, assinaturas atualizáveis"
  - "assinaturas atualizáveis, atualizar modos"
  - "assinaturas [replicação do SQL Server], atualizáveis"
ms.assetid: ab5ebab1-7ee4-41f4-999b-b4f0c420c921
caps.latest.revision: 38
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 38
---
# Alternar entre modos de atualiza&#231;&#227;o para uma assinatura transacional atualiz&#225;vel
  Este tópico descreve como alternar entre modos de atualização para uma assinatura de transação atualizável no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Especifique o modo para assinaturas atualizáveis usando o Assistente para Nova Assinatura. Para obter informações sobre como definir o modo ao usar esse assistente, consulte [Exibir e modificar propriedades de assinatura Pull](../../../relational-databases/replication/view-and-modify-pull-subscription-properties.md).  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Recomendações](#Recommendations)  
  
-   **Para alternar entre modos de atualização para uma assinatura transacional atualizável usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   É possível realizar failover da atualização imediata para a atualização em fila a qualquer momento. Entretanto, após fazê-lo, não será possível retornar para atualização imediata até que o Assinante ou o Publicador esteja conectado e o Queue Reader Agent tenha aplicado todas as mensagens pendentes na fila para o Publicador.  
  
###  <a name="Recommendations"></a> Recomendações  
  
-   Quando uma assinatura de atualização para uma publicação transacional oferecer suporte para failover de um modo de atualização para outro, você poderá alternar programaticamente os modos de atualização para tratar situações em que a conectividade muda por um curto intervalo de tempo. O modo de atualização pode ser definido programaticamente e sob demanda usando procedimentos armazenados de replicação. Para obter mais informações, consulte [Updatable Subscriptions for Transactional Replication](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md).  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
> [!NOTE]  
>  Para alterar o modo de atualização depois que a assinatura é criada, o **update_mode** propriedade deve ser definida como **failover** (que permite a troca de atualização imediata para atualização na fila) ou **failover na fila** (que permite a troca de atualização na fila para atualização imediata) quando a assinatura for criada. Essas propriedades são definidas automaticamente no Assistente para Nova Assinatura.  
  
#### Para definir o modo de atualização para uma assinatura push  
  
1.  Conecte-se ao Assinante no [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]e expanda o nó do servidor.  
  
2.  Expanda a pasta **Replicação** e, então, expanda a pasta **Assinaturas Locais** .  
  
3.  Clique com botão direito a assinatura para a qual você deseja definir o modo de atualização e, em seguida, clique em **definir o método Update**.  
  
4.  No **definir o método de atualização - \< assinante>: \< Banco_de_dados_de_assinatura>** caixa de diálogo, selecione **atualização imediata** ou **atualização na fila**.  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### Para definir o modo de atualização para uma assinatura pull  
  
1.  No **Propriedades de assinatura - \< publicador>: \< Banco_de_dados_de_publicação>** caixa de diálogo, selecione um valor de **imediatamente replicar alterações** ou **enfileirar alterações** para o **método de atualização do assinante** opção.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
 Para obter mais informações sobre como acessar o **Propriedades de assinatura - \< publicador>: \< Banco_de_dados_de_publicação>** caixa de diálogo, consulte [Exibir e modificar propriedades de assinatura Pull](../../../relational-databases/replication/view-and-modify-pull-subscription-properties.md).  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
  
#### Para alternar entre modos de atualização  
  
1.  Verifique se a assinatura oferece suporte a failover, executando [sp_helppullsubscription](../../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md) para uma assinatura pull ou [sp_helpsubscription](../../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md) para uma assinatura push. Se o valor de **o modo de atualização** no conjunto de resultados for **3** ou **4**, há suporte para failover.  
  
2.  No assinante no banco de dados de assinatura, execute [sp_setreplfailovermode](../../../relational-databases/system-stored-procedures/sp-setreplfailovermode-transact-sql.md). Especifique **@publisher**, **@publisher_db**, **@publication**, e um dos seguintes valores para **@failover_mode**:  
  
    -   **em fila** -failover para atualização em fila quando a conectividade for perdida temporariamente.  
  
    -   **imediata** -failover para atualização imediata quando conectividade foi restaurada.  
  
## Consulte também  
 [Updatable Subscriptions for Transactional Replication](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)  
  
  