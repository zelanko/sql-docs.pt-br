---
title: Definir opções de resolução de conflitos de atualização na fila (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- conflict resolution [SQL Server replication], queued updating subscriptions
- queued updating subscriptions [SQL Server replication]
ms.assetid: bb6b6c71-42c7-421a-a0fa-d5594d27e35d
caps.latest.revision: 34
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: df3e8c7450cf02e3b365e2d625d4844edac2fe35
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32959981"
---
# <a name="set-queued-updating-conflict-resolution-options-sql-server-management-studio"></a>Definir opções de resolução de conflito de atualização na fila (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Defina as opções de resolução de conflitos para publicações que dão suporte a assinaturas de atualização na fila na página **Opções de Assinatura** da caixa de diálogo **Propriedades de Publicação – \<Publicação>**. Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
### <a name="to-set-queued-updating-conflict-resolution-options"></a>Para definir opções de resolução de conflito de atualização na fila  
  
1.  Na página **Opções de Assinatura** da caixa de diálogo **Propriedades de Publicação – \<Publicação>**, selecione um dos seguintes valores para a opção **Política de resolução de conflitos**:  
  
    -   **Mantenha a alteração do Publicador.**  
  
    -   **Mantenha a alteração do Assinante.**  
  
    -   **Reinicialize a assinatura.**  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Habilitar atualização de assinaturas para publicações transacionais](../../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md)   
 [Queued Updating Conflict Detection and Resolution](../../../relational-databases/replication/transactional/updatable-subscriptions-queued-updating-conflict-resolution.md)  
  
  
