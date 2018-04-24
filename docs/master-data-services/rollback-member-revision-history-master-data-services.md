---
title: Reverger histórico de revisões do membro (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: ''
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d39d3474-20e7-429f-9c8d-fcc4eb0854fc
caps.latest.revision: 5
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3b4291383c9f2f1d41ea13997f2feeb6e7c1014d
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="rollback-member-revision-history-master-data-services"></a>Reverter Histórico de Revisões do Membro (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Um histórico de revisões do membro é registrado sempre que um membro é alterado. Você pode reverter um histórico de revisões do membro para uma versão anterior.  
  
## <a name="prerequisites"></a>Prerequisites  
  
-   Você deve ter permissão para atualizar pelo menos um dos atributos do membro selecionado. Quando você reverter um histórico de revisões, todos os valores do atributo que podem ser atualizados serão revertidos para os valores da versão anterior.  
  
-   O histórico de revisões só estará disponível quando o tipo do log de transações da entidade for um membro.  
  
 **Para reverter um histórico de revisões do membro**  
  
1.  No Master Data Manager, clique em Explorer.  
  
2.  Escolha a entidade e o membro para a reversão.  
  
3.  Clique em **Exibir Histórico.**  
  
4.  Escolha a revisão para reverter e, em seguida, clique em **Reverter**.  
  
## <a name="see-also"></a>Consulte Também  
 [Histórico de revisão de membro &#40;Master Data Services&#41;](../master-data-services/member-revision-history-master-data-services.md)   
 [Alterar o tipo de log de transações de entidade &#40;Master Data Services&#41;](../master-data-services/change-the-entity-transaction-log-type-master-data-services.md)  
  
  
