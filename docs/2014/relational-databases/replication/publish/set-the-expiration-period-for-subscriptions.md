---
title: Definir o período de expiração da assinatura | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [SQL Server replication], expiration
- expiration [SQL Server replication]
- retention periods [SQL Server replication]
- deactivating subscriptions
ms.assetid: 542f0613-5817-42d0-b841-fb2c94010665
caps.latest.revision: 34
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 95cdae09ead5238e8a48d3797f2b1f9a32b483f3
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37268922"
---
# <a name="set-the-expiration-period-for-subscriptions"></a>Definir o período de validade da assinatura
  Este tópico descreve como definir o período de validade para assinaturas no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../../includes/tsql-md.md)]. O período de validade das assinaturas determina o período de tempo antes de uma assinatura expirar e ser removida. Para obter mais informações, consulte [Subscription Expiration and Deactivation](../subscription-expiration-and-deactivation.md).  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Recomendações](#Recommendations)  
  
-   **Para definir o período de validade da assinatura, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Recommendations"></a> Recomendações  
  
-   O período de validade da assinatura também é referenciado como o *período de retenção da publicação*. A limpeza dos metadados de replicação de mesclagem depende dessa configuração:  
  
    -   A replicação não poderá limpar os metadados na publicação e nos bancos de dados de assinatura antes de o período de retenção ser atingido. Cuidado ao especificar um valor alto para o período de retenção, pois poderá impactar negativamente o desempenho da replicação. Recomendamos que use uma definição mais baixa se puder prevenir com certeza que todos os Assinantes sincronizarão normalmente dentro daquele período de tempo.  
  
         O período de retenção para publicações de mesclagem tem um período de tolerância de 24 horas para incluir os Assinantes em fusos horários diferentes. Por exemplo, se você definir um período de retenção de um dia, o período de retenção real será de 48 horas.  
  
    -   É possível especificar para que as assinaturas nunca expirem, mas recomendamos não usar este valor, pois os metadados não poderão ser limpos.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Defina o período de expiração da assinatura na página **Geral** da caixa de diálogo **Propriedades de Publicação – \<Publicação>**. Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [View and Modify Publication Properties](view-and-modify-publication-properties.md).  
  
#### <a name="to-set-the-expiration-period-for-subscriptions"></a>Para definir o período de validade da assinatura  
  
1.  Na seção **Expiração da assinatura** na página **Geral** da caixa de diálogo **Propriedades de Publicação – \<Publicação>**, especifique se as assinaturas devem expirar.  
  
2.  Caso devam vencer, especifique um período de tempo para o vencimento.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
 Você pode usar os procedimentos armazenados de replicação para definir este valor quando uma publicação é criada ou para modificar este valor posteriormente.  
  
#### <a name="to-set-the-expiration-period-for-a-subscription-to-a-snapshot-or-transactional-publication"></a>Para definir o período de validade de uma assinatura de um instantâneo ou publicação transacional  
  
1.  No Publicador, execute [sp_addpublication](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql). Especifique o período de validade de assinatura desejado, em horas, para **@retention**. O período de validade padrão é de 336 horas. Para obter mais informações, consulte [Create a Publication](create-a-publication.md).  
  
#### <a name="to-set-the-expiration-period-for-a-subscription-to-a-merge-publication"></a>Para definir o período de validade para uma assinatura de uma publicação de mesclagem  
  
1.  No Publicador, execute [sp_addmergepublication](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql). Especifique o valor desejado para o período de validade da assinatura como **@retention**. Especifique as unidades nas quais o período de validade é expressado para **@retention_period_unit**, que pode ser um dos seguintes:  
  
    -   **1** = semana  
  
    -   **2** = mês  
  
    -   **3** = ano  
  
     O período de validade padrão é de 14 dias. Para obter mais informações, consulte [Create a Publication](create-a-publication.md).  
  
#### <a name="to-change-the-expiration-period-for-a-subscription-to-a-snapshot-or-transactional-publication"></a>Para alterar o período de validade de uma assinatura de um instantâneo ou publicação transacional  
  
1.  No Publicador, execute [sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql). Especifique a **retenção** para **@property** e o novo período de validade da assinatura, em horas, para **@value**.  
  
#### <a name="to-change-the-expiration-period-for-a-subscription-to-a-merge-publication"></a>Para alterar o período de validade para uma assinatura de uma publicação de mesclagem  
  
1.  No Publicador, execute [sp_helpmergepublication](/sql/relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql), especificando **@publication** e **@publisher**. Observe o valor de **retention_period_unit** no conjunto de resultados que pode ser um dos seguintes:  
  
    -   **0** = dia|  
  
    -   **1** = semana  
  
    -   **2** = mês  
  
    -   **3** = ano  
  
2.  No Publicador, execute [sp_changemergepublication](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql). Especifique a **retenção** para **@property** e o novo período de validade da assinatura, com base no texto sobre unidade de período de retenção da etapa 1, para **@value**.  
  
3.  (Opcional) No Editor, execute [sp_changemergepublication](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql). Especifique a **retention_period_unit** para **@property** e uma nova unidade para o período de validade da assinatura para **@value**.  
  
## <a name="see-also"></a>Consulte também  
 [Replication System Stored Procedures Concepts](../concepts/replication-system-stored-procedures-concepts.md)   
 [Subscription Expiration and Deactivation](../subscription-expiration-and-deactivation.md)  
  
  
