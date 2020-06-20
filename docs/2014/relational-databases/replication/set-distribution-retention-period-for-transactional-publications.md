---
title: Definir o período de retenção de distribuição para publicações transacionais (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- transaction retention periods [SQL Server replication]
- retention periods [SQL Server replication]
ms.assetid: 9a98c53a-fea5-4235-b23d-6c69587c5676
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a68f092c63e75196ab82a81d2a8ca36d13142813
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85055672"
---
# <a name="set-the-distribution-retention-period-for-transactional-publications-sql-server-management-studio"></a>Definir o período de retenção de distribuição para publicações transacionais (SQL Server Management Studio)
  Especifique o período mínimo de retenção de distribuição e o período máximo de retenção de distribuição na caixa de diálogo **Propriedades do banco de \<DistributionDatabase> dados de distribuição** . Isso está disponível na página **geral** da caixa de diálogo **Propriedades do \<Distributor> distribuidor –** . Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [Exibir e modificar as propriedades do Distribuidor e do Publicador](view-and-modify-distributor-and-publisher-properties.md).  
  
### <a name="to-specify-the-distribution-retention-period"></a>Para especificar o período de retenção de distribuição  
  
1.  Na página **geral** da caixa de diálogo **Propriedades do \<Distributor> distribuidor –** , clique no botão de Propriedades (**...**) para o banco de dados de distribuição.  
  
2.  Para especificar o período mínimo de retenção de distribuição, insira um valor na caixa **Pelo menos** ; para especificar o período máximo de retenção de distribuição, insira um valor na caixa **Mas não mais de** .  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar a distribuição](configure-distribution.md)   
 [Validade e desativação de assinatura](subscription-expiration-and-deactivation.md)  
  
  
