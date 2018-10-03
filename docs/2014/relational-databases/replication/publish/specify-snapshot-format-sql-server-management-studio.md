---
title: Especificar o formato do instantâneo (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], formats
- snapshot replication [SQL Server], formats
ms.assetid: 7c95f545-731a-4743-9acb-0b325ef9b98b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: fe570f8e23d933dfc1974564401069305e9a88a3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48199926"
---
# <a name="specify-snapshot-format-sql-server-management-studio"></a>Especificar o formato do instantâneo (SQL Server Management Studio)
  Especifique o formato do instantâneo na página **Instantâneo** da caixa de diálogo **Propriedades de Publicação – \<Publicação>**. Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [View and Modify Publication Properties](view-and-modify-publication-properties.md).  
  
### <a name="to-specify-snapshot-format"></a>Para especificar o formato do instantâneo  
  
1.  Na página **Instantâneo** da caixa de diálogo **Propriedades da Publicação – \<Publicação>**, selecione **SQL Server Nativo – todos os Assinantes devem ser servidores que executam o SQL Server** ou **Caractere – necessário se um Publicador ou Assinante não executar o SQL Server**.  
  
    > [!NOTE]  
    >  É recomendável a seleção do formato nativo, a menos que essa publicação deva dar suporte a assinaturas de um banco de dados [!INCLUDE[ssEW](../../../includes/ssew-md.md)] ou um banco de dados não[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Configurar propriedades de instantâneo &#40;Programação Transact-SQL de Replicação&#41;](configure-snapshot-properties-replication-transact-sql-programming.md)   
 [Alterar propriedades da publicação e do artigo](change-publication-and-article-properties.md)   
 [Inicializar uma assinatura com um instantâneo](../initialize-a-subscription-with-a-snapshot.md)  
  
  
