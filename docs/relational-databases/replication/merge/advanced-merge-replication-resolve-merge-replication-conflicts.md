---
title: "Detectar e resolver conflitos de replicação de mesclagem | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], about conflict resolution
- default conflict resolver
- conflict resolution [SQL Server replication]
- viewing merge replication conflicts
- resolving merge replication conflicts
- articles [SQL Server replication], conflict resolution
- merge replication conflict resolution [SQL Server replication]
- conflict resolution [SQL Server replication], merge replication
ms.assetid: 0d033c76-e8c9-4e35-ab95-4d335abb18c1
caps.latest.revision: 37
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: ea0d016f2fc6e73be6458ed44f34f42dfbd140bf
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="advanced-merge-replication---resolve-merge-replication-conflicts"></a>Replicação de mesclagem avançada – resolver conflitos de replicação de mesclagem
  Quando o Publicador e o Assinante estão conectados e ocorre a sincronização, o Agente de Mesclagem detecta se há algum conflito. Se houver conflitos detectados, o Agente de Mesclagem utiliza um resolvedor de conflitos para determinar quais dados serão aceitos e propagados para outros sites.  
  
> [!NOTE]  
>  Embora o Assinante esteja sincronizado com o Publicador, os conflitos ocorrem normalmente entre as atualizações feitas em diferentes Assinantes, em lugar de atualizações feitas no Assinante e no Publicador.  
  
 A replicação de mesclagem oferece uma variedade de métodos para detectar e resolver conflitos. Com relação à maioria dos aplicativos, o método padrão é apropriado.  
  
-   Se um conflito ocorrer entre um Publicador e um Assinante, a alteração do Publicador é mantida e a alteração do Assinante é descartada.  
  
-   Se ocorrer um conflito entre dois Assinantes que usam assinaturas de cliente (tipo padrão para assinaturas pull), a alteração do primeiro Assinante para sincronizar com o Publicador é mantida, e a alteração do segundo Assinante é descartada. Para obter informações sobre como especificar assinatura de cliente e servidor, consulte [Especificar um tipo de assinatura de mesclagem e prioridade de resolução de conflitos &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/specify-a-merge-subscription-type-and-conflict-resolution-priority.md).  
  
-   Em caso de conflito entre dois Assinantes que usam assinaturas de servidor (tipo padrão para assinaturas push), a alteração do Assinante com o maior valor da prioridade será mantida, e a alteração do segundo Assinante será descartada. Se os valores de prioridade forem iguais, a alteração do primeiro Assinante a sincronizar com o Publicador será mantida.  
  
 Para obter mais informações sobre a detecção de conflito e resolução para replicação de mesclagem, consulte [Advanced Merge Replication Conflict Detection and Resolution](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md).  
  
## <a name="see-also"></a>Consulte também  
 [Opções de artigos para a replicação de mesclagem](../../../relational-databases/replication/merge/article-options-for-merge-replication.md)   
 [Assinar Publicações](../../../relational-databases/replication/subscribe-to-publications.md)  
  
  
