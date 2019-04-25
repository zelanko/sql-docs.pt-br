---
title: Conjuntos de alterações (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: f227c49a-ed46-4e0f-8992-83093456cf94
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: f5cee5122ca28c8eb16f3b7b0b4d1b330f5777b4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62508824"
---
# <a name="changesets-master-data-services"></a>Conjuntos de alterações (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] agora dá suporte à capacidade de salvar todas as alterações pendentes em uma entidade como conjuntos de alterações. Há dois cenários de uso para este recurso.  
  
-   **É alterado quando "Aprovação necessária" é ativada pelo Administrador de Entidade**  
  
     Se um Administrador de entidade especificar que as alterações em determinada entidade exigem aprovação antes que sejam confirmadas, as alterações na entidade deverão ser salvas em um conjunto de alterações novo ou existente antes que sejam enviadas para aprovação.  Para obter mais informações, consulte [Aprovação necessária &#40;Master Data Services&#41;](../master-data-services/approval-required-master-data-services.md)  
  
     Siga este fluxo de trabalho.  
  
    1.  Crie um conjunto de alterações. O conjunto de alterações está no estado Em aberto. Consulte [Criar um conjunto de alterações &#40;Master Data Services&#41;](../master-data-services/create-a-changeset-master-data-services.md)  
  
    2.  Aplique o conjunto de alterações e adicione algumas alterações ao conjunto de alterações. Consulte [Aplicar e atualizar um conjunto de alterações &#40;Master Data Services&#41;](../master-data-services/apply-and-update-a-changeset-master-data-services.md)  
  
    3.  Você envia o conjunto de alterações para o administrador de entidade para aprovação. O conjunto de alterações está no estado Pendente. Consulte [Confirmar ou enviar um conjunto de alterações &#40;Master Data Services&#41;](../master-data-services/commit-or-submit-a-changeset-master-data-services.md)  
  
    4.  O administrador de entidade obtém uma notificação por email indicando que um conjunto de alterações está aguardando aprovação. Se o administrador de entidade aprovar o conjunto de alterações, ele estará no estado Aprovado. Consulte [Aprovar ou rejeitar um conjunto de alterações &#40;Master Data Services&#41;](../master-data-services/approve-or-reject-a-changeset-master-data-services.md)  
  
    5.  O conjunto de alterações aprovado será confirmado automaticamente. Se a alteração for confirmada com êxito, o conjunto de alterações estará no estado confirmado.  
  
-   **Alterações do usuário local**  
  
     Se você quiser apenas salvar as alterações locais para que possa usá-las ou recuperá-las mais tarde, será possível usar conjuntos de alterações para conseguir isso.  
  
     Siga este fluxo de trabalho.  
  
    1.  Crie um conjunto de alterações. O conjunto de alterações está no estado Em aberto. Consulte [Criar um conjunto de alterações &#40;Master Data Services&#41;](../master-data-services/create-a-changeset-master-data-services.md)  
  
    2.  Aplique o conjunto de alterações e adicione algumas alterações ao conjunto de alterações. Consulte [Aplicar e atualizar um conjunto de alterações &#40;Master Data Services&#41;](../master-data-services/apply-and-update-a-changeset-master-data-services.md)  
  
    3.  Quando estiver pronto, você confirma o conjunto de alterações. Consulte [Confirmar ou enviar um conjunto de alterações &#40;Master Data Services&#41;](../master-data-services/commit-or-submit-a-changeset-master-data-services.md)  
  
## <a name="see-also"></a>Consulte também  
 [Criar um conjunto de alterações &#40;Master Data Services&#41;](../master-data-services/create-a-changeset-master-data-services.md)   
 [Aplicar e atualizar um conjunto de alterações &#40;Master Data Services&#41;](../master-data-services/apply-and-update-a-changeset-master-data-services.md)   
 [Confirmar ou enviar um conjunto de alterações &#40;Master Data Services&#41;](../master-data-services/commit-or-submit-a-changeset-master-data-services.md)   
 [Aprovar ou rejeitar um conjunto de alterações &#40;Master Data Services&#41;](../master-data-services/approve-or-reject-a-changeset-master-data-services.md)   
 [Gerenciar conjuntos de alterações &#40;Master Data Services&#41;](../master-data-services/manage-changesets-master-data-services.md)  
  
  
