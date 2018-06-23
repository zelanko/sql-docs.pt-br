---
title: Definir opções de resolução de conflitos de atualização na fila (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- conflict resolution [SQL Server replication], queued updating subscriptions
- queued updating subscriptions [SQL Server replication]
ms.assetid: bb6b6c71-42c7-421a-a0fa-d5594d27e35d
caps.latest.revision: 32
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: d4b372dc750822d965474d93d40ff7911cf0cf7c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36012876"
---
# <a name="set-queued-updating-conflict-resolution-options-sql-server-management-studio"></a>Definir opções de resolução de conflito de atualização na fila (SQL Server Management Studio)
  Defina as opções de resolução de conflitos para publicações que dão suporte a assinaturas de atualização na fila na página **Opções de Assinatura** da caixa de diálogo **Propriedades de Publicação – \<Publicação>**. Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [View and Modify Publication Properties](view-and-modify-publication-properties.md).  
  
### <a name="to-set-queued-updating-conflict-resolution-options"></a>Para definir opções de resolução de conflito de atualização na fila  
  
1.  Na página **Opções de Assinatura** da caixa de diálogo **Propriedades de Publicação – \<Publicação>**, selecione um dos seguintes valores para a opção **Política de resolução de conflitos**:  
  
    -   **Mantenha a alteração do Publicador.**  
  
    -   **Mantenha a alteração do Assinante.**  
  
    -   **Reinicialize a assinatura.**  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Habilitar atualização de assinaturas para publicações transacionais](enable-updating-subscriptions-for-transactional-publications.md)   
 [Queued Updating Conflict Detection and Resolution](../transactional/updatable-subscriptions-queued-updating-conflict-resolution.md)  
  
  