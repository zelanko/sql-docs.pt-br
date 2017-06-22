---
title: "Especificar o formato do instantâneo (SQL Server Management Studio) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- snapshots [SQL Server replication], formats
- snapshot replication [SQL Server], formats
ms.assetid: 7c95f545-731a-4743-9acb-0b325ef9b98b
caps.latest.revision: 38
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6b826abf097e54346bd300b54ecb6697515f8564
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="specify-snapshot-format-sql-server-management-studio"></a>Especificar o formato do instantâneo (SQL Server Management Studio)
  Especifique o formato do instantâneo na página **Instantâneo** da caixa de diálogo **Propriedades de Publicação – \<Publicação>**. Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
### <a name="to-specify-snapshot-format"></a>Para especificar o formato do instantâneo  
  
1.  Na página **Instantâneo** da caixa de diálogo **Propriedades da Publicação – \<Publicação>**, selecione **SQL Server Nativo – todos os Assinantes devem ser servidores que executam o SQL Server** ou **Caractere – necessário se um Publicador ou Assinante não executar o SQL Server**.  
  
    > [!NOTE]  
    >  É recomendável a seleção do formato nativo, a menos que essa publicação deva dar suporte a assinaturas de um banco de dados [!INCLUDE[ssEW](../../../includes/ssew-md.md)] ou um banco de dados não[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Configurar propriedades de instantâneo &#40;Programação Transact-SQL de Replicação&#41;](../../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)   
 [Alterar propriedades da publicação e do artigo](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [Inicializar uma assinatura com um instantâneo](../../../relational-databases/replication/initialize-a-subscription-with-a-snapshot.md)  
  
  
