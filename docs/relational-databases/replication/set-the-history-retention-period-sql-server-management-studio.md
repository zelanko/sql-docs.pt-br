---
title: Definir o período de retenção do histórico (SSMS)
description: Saiba como definir o período de retenção do histórico do banco de dados de distribuição no SSMS (SQL Server Management Studio).
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- history retention periods [SQL Server replication]
- retention periods [SQL Server replication]
ms.assetid: c288daab-5181-4d4b-ba2a-8a147098e758
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 6f9ada00c3166637ca1c5721b17ed950df58a4e2
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "76287193"
---
# <a name="set-the-history-retention-period-sql-server-management-studio"></a>Definir o período de retenção do histórico (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  Especifique o período de retenção de histórico na página **Geral** da caixa de diálogo **Propriedades do Banco de Dados de Distribuição – \<DistributionDatabase>** . Essa configuração controla o tempo durante o qual o histórico do agente de replicação fica armazenado. Essa página está disponível na página **Geral** da caixa de diálogo **Propriedades do Distribuidor – \<Distribuidor>** . Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [Exibir e modificar as propriedades do Distribuidor e do Publicador](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md).  
  
### <a name="to-specify-the-history-retention-period"></a>Para especificar o período de retenção do histórico  
  
1.  Na página **Geral** da caixa de diálogo **Propriedades do Distribuidor – \<Distribuidor>** , clique no botão de propriedades ( **…** ) do banco de dados do distribuidor.  
  
2.  Insira um valor na caixa **Armazenar histórico de desempenho de replicação pelo menos** .  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar Distribuição](../../relational-databases/replication/configure-distribution.md)  
  
  
