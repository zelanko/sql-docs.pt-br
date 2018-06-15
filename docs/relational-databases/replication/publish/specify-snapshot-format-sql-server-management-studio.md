---
title: Especificar o formato do instantâneo (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- snapshots [SQL Server replication], formats
- snapshot replication [SQL Server], formats
ms.assetid: 7c95f545-731a-4743-9acb-0b325ef9b98b
caps.latest.revision: 38
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 995bf55405498ac38105464b6829eed5b85425be
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32959767"
---
# <a name="specify-snapshot-format-sql-server-management-studio"></a>Especificar o formato do instantâneo (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Especifique o formato do instantâneo na página **Instantâneo** da caixa de diálogo **Propriedades de Publicação – \<Publicação>**. Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
### <a name="to-specify-snapshot-format"></a>Para especificar o formato do instantâneo  
  
1.  Na página **Instantâneo** da caixa de diálogo **Propriedades da Publicação – \<Publicação>**, selecione **SQL Server Nativo – todos os Assinantes devem ser servidores que executam o SQL Server** ou **Caractere – necessário se um Publicador ou Assinante não executar o SQL Server**.  
  
    > [!NOTE]  
    >  É recomendável a seleção do formato nativo, a menos que essa publicação deva dar suporte a assinaturas de um banco de dados [!INCLUDE[ssEW](../../../includes/ssew-md.md)] ou um banco de dados não[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar propriedades de instantâneo &#40;Programação Transact-SQL de Replicação&#41;](../../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)   
 [Alterar propriedades da publicação e do artigo](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [Inicializar uma assinatura com um instantâneo](../../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
  
  
