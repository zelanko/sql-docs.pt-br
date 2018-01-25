---
title: "Definir o período de retenção do histórico (SQL Server Management Studio) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
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
- history retention periods [SQL Server replication]
- retention periods [SQL Server replication]
ms.assetid: c288daab-5181-4d4b-ba2a-8a147098e758
caps.latest.revision: "36"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4b43e9ee27b6121bf9bc35107ade4a09a6808fa7
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2018
---
# <a name="set-the-history-retention-period-sql-server-management-studio"></a>Definir o período de retenção do histórico (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Especifique o período de retenção de histórico na página **Geral** da caixa de diálogo **Propriedades do Banco de Dados de Distribuição – \<DistributionDatabase>**. Essa configuração controla o tempo durante o qual o histórico do agente de replicação fica armazenado. Essa página está disponível na página **Geral** da caixa de diálogo **Propriedades do Distribuidor – \<Distribuidor>**. Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [Exibir e modificar as propriedades do Distribuidor e do Publicador](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md).  
  
### <a name="to-specify-the-history-retention-period"></a>Para especificar o período de retenção do histórico  
  
1.  Na página **Geral** da caixa de diálogo **Propriedades do Distribuidor – \<Distribuidor>**, clique no botão de propriedades (**…**) do banco de dados do distribuidor.  
  
2.  Insira um valor na caixa **Armazenar histórico de desempenho de replicação pelo menos** .  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar Distribuição](../../relational-databases/replication/configure-distribution.md)  
  
  
