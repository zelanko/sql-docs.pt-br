---
title: Definir o período de expiração da assinatura | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [SQL Server replication], expiration
- expiration [SQL Server replication]
- retention periods [SQL Server replication]
- deactivating subscriptions
ms.assetid: 542f0613-5817-42d0-b841-fb2c94010665
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 663de184c811291c4b583ddbaf2fb6862097c54f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "73882174"
---
# <a name="set-the-expiration-period-for-subscriptions"></a>Definir o período de validade da assinatura
  Este tópico descreve como definir o período de validade para assinaturas no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../../includes/tsql-md.md)]. O período de validade das assinaturas determina o período de tempo antes de uma assinatura expirar e ser removida. Para obter mais informações, consulte [Subscription Expiration and Deactivation](../subscription-expiration-and-deactivation.md).  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Recomendações](#Recommendations)  
  
-   **Para definir o período de validade da assinatura, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> Recomendações  
  
-   O período de validade da assinatura também é referenciado como o *período de retenção da publicação*. A limpeza dos metadados de replicação de mesclagem depende dessa configuração:  
  
    -   A replicação não poderá limpar os metadados na publicação e nos bancos de dados de assinatura antes de o período de retenção ser atingido. Cuidado ao especificar um valor alto para o período de retenção, pois poderá impactar negativamente o desempenho da replicação. Recomendamos que use uma definição mais baixa se puder prevenir com certeza que todos os Assinantes sincronizarão normalmente dentro daquele período de tempo.  
  
         O período de retenção para publicações de mesclagem tem um período de tolerância de 24 horas para incluir os Assinantes em fusos horários diferentes. Por exemplo, se você definir um período de retenção de um dia, o período de retenção real será de 48 horas.  
  
    -   É possível especificar para que as assinaturas nunca expirem, mas recomendamos não usar este valor, pois os metadados não poderão ser limpos.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Defina o período de expiração da assinatura na página **Geral** da caixa de diálogo **Propriedades de Publicação – \<Publicação>** . Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [View and Modify Publication Properties](view-and-modify-publication-properties.md).  
  
#### <a name="to-set-the-expiration-period-for-subscriptions"></a>Para definir o período de validade da assinatura  
  
1.  Na seção **Expiração da assinatura** na página **Geral** da caixa de diálogo **Propriedades de Publicação – \<Publicação>** , especifique se as assinaturas devem expirar.  
  
2.  Caso devam vencer, especifique um período de tempo para o vencimento.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
 Você pode usar os procedimentos armazenados de replicação para definir este valor quando uma publicação é criada ou para modificar este valor posteriormente.  
  
#### <a name="to-set-the-expiration-period-for-a-subscription-to-a-snapshot-or-transactional-publication"></a>Para definir o período de validade de uma assinatura de um instantâneo ou publicação transacional  
  
1.  No Publicador, execute [sp_addpublication](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql). Especifique o período de validade de assinatura desejado, em horas, em **\@retention**. O período de validade padrão é de 336 horas. Para obter mais informações, consulte [Criar uma assinatura](create-a-publication.md).  
  
#### <a name="to-set-the-expiration-period-for-a-subscription-to-a-merge-publication"></a>Para definir o período de validade para uma assinatura de uma publicação de mesclagem  
  
1.  No Publicador, execute [sp_addmergepublication](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql). Especifique o valor desejado para o período de validade da assinatura em **\@retention**. Especifique as unidades nas quais o período de validade é expresso em **\@retention_period_unit**, que pode ser um dos seguintes:  
  
    -   **1** = semana  
  
    -   **2** = mês  
  
    -   **3** = ano  
  
     O período de validade padrão é de 14 dias. Para obter mais informações, consulte [Criar uma assinatura](create-a-publication.md).  
  
#### <a name="to-change-the-expiration-period-for-a-subscription-to-a-snapshot-or-transactional-publication"></a>Para alterar o período de validade de uma assinatura de um instantâneo ou publicação transacional  
  
1.  No Publicador, execute [sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql). Especifique **retention** em **\@property** e o novo período de validade da assinatura, em horas, em **\@value**.  
  
#### <a name="to-change-the-expiration-period-for-a-subscription-to-a-merge-publication"></a>Para alterar o período de validade para uma assinatura de uma publicação de mesclagem  
  
1.  No Publicador, execute [sp_helpmergepublication](/sql/relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql) especificando **\@publication** e **\@publisher**. Observe o valor de **retention_period_unit** no conjunto de resultados que pode ser um dos seguintes:  
  
    -   **0** = dia|  
  
    -   **1** = semana  
  
    -   **2** = mês  
  
    -   **3** = ano  
  
2.  No Publicador, execute [sp_changemergepublication](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql). Especifique **retention** em **\@property** e o novo período de validade da assinatura, como texto com base na unidade de período de retenção da etapa 1, em **\@value**.  
  
3.  (Opcional) No Editor, execute [sp_changemergepublication](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql). Especifique **retention_period_unit** em **\@property** e uma nova unidade para o período de validade da assinatura em **\@value**.  
  
## <a name="see-also"></a>Consulte Também  
 [Replication System Stored Procedures Concepts](../concepts/replication-system-stored-procedures-concepts.md)   
 [Desativação e expiração de assinatura](../subscription-expiration-and-deactivation.md)  
  
  
