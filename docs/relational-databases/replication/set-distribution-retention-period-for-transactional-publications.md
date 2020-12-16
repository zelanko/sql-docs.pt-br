---
title: Definir o período de retenção da distribuição
description: Defina o período de retenção para os dados no banco de dados de distribuição do SSMS (SQL Server Management Studio).
ms.custom: seo-lt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- transaction retention periods [SQL Server replication]
- retention periods [SQL Server replication]
ms.assetid: 9a98c53a-fea5-4235-b23d-6c69587c5676
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016
ms.openlocfilehash: a5f1f925d4ab0438ab237a903b2ad80007e86e20
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97479727"
---
# <a name="set-distribution-retention-period-for-transactional-publications"></a>Definir o período de retenção de distribuição para publicações transacionais
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  Especifique o período mínimo de retenção da distribuição e o período máximo de retenção da distribuição na caixa de diálogo **Propriedades do Banco de Dados de Distribuição – \<DistributionDatabase>** . Isso está disponível na página **Geral** da caixa de diálogo **Propriedades do Distribuidor – \<Distributor>** . Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [Exibir e modificar as propriedades do Distribuidor e do Publicador](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md).  
  
### <a name="to-specify-the-distribution-retention-period"></a>Para especificar o período de retenção de distribuição  
  
1.  Na página **Geral** da caixa de diálogo **Propriedades do Distribuidor – \<Distributor>** , clique no botão de propriedades ( **...** ) do banco de dados de distribuição.  
  
2.  Para especificar o período mínimo de retenção de distribuição, insira um valor na caixa **Pelo menos** ; para especificar o período máximo de retenção de distribuição, insira um valor na caixa **Mas não mais de** .  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

## <a name="see-also"></a>Consulte Também  
 [Configurar Distribuição](../../relational-databases/replication/configure-distribution.md)   
 [Desativação e expiração de assinatura](../../relational-databases/replication/subscription-expiration-and-deactivation.md)  
  
  
