---
title: "Definir o período de retenção de distribuição para publicações transacionais | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- transaction retention periods [SQL Server replication]
- retention periods [SQL Server replication]
ms.assetid: 9a98c53a-fea5-4235-b23d-6c69587c5676
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3a4c7ebac3ab29e62d633f03891014f6088f2711
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/08/2018
---
# <a name="set-distribution-retention-period-for-transactional-publications"></a>Definir o período de retenção de distribuição para publicações transacionais
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Especifique o período mínimo de retenção da distribuição e o período máximo de retenção da distribuição na caixa de diálogo **Propriedades do Banco de Dados de Distribuição – \<DistributionDatabase>**. Está disponível na página **Geral** da caixa de diálogo **Propriedades do Distribuidor – \<Distribuidor>**. Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [Exibir e modificar as propriedades do Distribuidor e do Publicador](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md).  
  
### <a name="to-specify-the-distribution-retention-period"></a>Para especificar o período de retenção de distribuição  
  
1.  Na página **Geral** da caixa de diálogo **Propriedades do Distribuidor – \<Distribuidor>**, clique no botão de propriedades (**…**) do banco de dados do distribuidor.  
  
2.  Para especificar o período mínimo de retenção de distribuição, insira um valor na caixa **Pelo menos** ; para especificar o período máximo de retenção de distribuição, insira um valor na caixa **Mas não mais de** .  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar Distribuição](../../relational-databases/replication/configure-distribution.md)   
 [Desativação e expiração de assinatura](../../relational-databases/replication/subscription-expiration-and-deactivation.md)  
  
  
