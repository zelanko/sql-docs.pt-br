---
title: "Reverger histórico de revisões do membro (Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d39d3474-20e7-429f-9c8d-fcc4eb0854fc
caps.latest.revision: 5
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: a242f91eb8259b8941a61db94f59c4e331d5b06b
ms.contentlocale: pt-br
ms.lasthandoff: 09/07/2017

---
# <a name="rollback-member-revision-history-master-data-services"></a>Reverter Histórico de Revisões do Membro (Master Data Services)
  Um histórico de revisões do membro é registrado sempre que um membro é alterado. Você pode reverter um histórico de revisões do membro para uma versão anterior.  
  
## <a name="prerequisites"></a>Pré-requisitos  
  
-   Você deve ter permissão para atualizar pelo menos um dos atributos do membro selecionado. Quando você reverter um histórico de revisões, todos os valores do atributo que podem ser atualizados serão revertidos para os valores da versão anterior.  
  
-   O histórico de revisões só estará disponível quando o tipo do log de transações da entidade for um membro.  
  
 **Para reverter um histórico de revisões do membro**  
  
1.  No Master Data Manager, clique em Explorer.  
  
2.  Escolha a entidade e o membro para a reversão.  
  
3.  Clique em **Exibir Histórico.**  
  
4.  Escolha a revisão para reverter e, em seguida, clique em **Reverter**.  
  
## <a name="see-also"></a>Consulte também  
 [Histórico de revisão de membro &#40;Master Data Services&#41;](../master-data-services/member-revision-history-master-data-services.md)   
 [Alterar o tipo de log de transações de entidade &#40;Master Data Services&#41;](../master-data-services/change-the-entity-transaction-log-type-master-data-services.md)  
  
  

