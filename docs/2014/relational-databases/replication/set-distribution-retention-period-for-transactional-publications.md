---
title: Definir o período de retenção de distribuição para publicações transacionais (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- transaction retention periods [SQL Server replication]
- retention periods [SQL Server replication]
ms.assetid: 9a98c53a-fea5-4235-b23d-6c69587c5676
caps.latest.revision: 35
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: ad1a697d6e139939723296fd481b2bbdb15cc39e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36019551"
---
# <a name="set-the-distribution-retention-period-for-transactional-publications-sql-server-management-studio"></a>Definir o período de retenção de distribuição para publicações transacionais (SQL Server Management Studio)
  Especifique o período mínimo de retenção da distribuição e o período máximo de retenção da distribuição na caixa de diálogo **Propriedades do Banco de Dados de Distribuição – \<DistributionDatabase>**. Está disponível na página **Geral** da caixa de diálogo **Propriedades do Distribuidor – \<Distribuidor>**. Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [Exibir e modificar as propriedades do Distribuidor e do Publicador](view-and-modify-distributor-and-publisher-properties.md).  
  
### <a name="to-specify-the-distribution-retention-period"></a>Para especificar o período de retenção de distribuição  
  
1.  Na página **Geral** da caixa de diálogo **Propriedades do Distribuidor – \<Distribuidor>**, clique no botão de propriedades (**…**) do banco de dados do distribuidor.  
  
2.  Para especificar o período mínimo de retenção de distribuição, insira um valor na caixa **Pelo menos** ; para especificar o período máximo de retenção de distribuição, insira um valor na caixa **Mas não mais de** .  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Configurar Distribuição](configure-distribution.md)   
 [Desativação e expiração de assinatura](subscription-expiration-and-deactivation.md)  
  
  