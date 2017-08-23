---
title: "Bloquear uma versão (Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- versions [Master Data Services], locking
- locking versions [Master Data Services]
ms.assetid: 7bb62a84-12d8-4b29-9b6e-6aa25410618e
caps.latest.revision: 7
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8edd7ce020ad20917c4bdc76c636b8cf7a06fadd
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="lock-a-version-master-data-services"></a>Bloquear uma versão (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], bloqueie uma versão de um modelo para evitar alterações nos membros do modelo e em seus atributos.  
  
> [!NOTE]  
>  Quando uma versão estiver bloqueada, os administradores do modelo poderão continuar adicionando, editando e removendo membros. Outros usuários com permissão para o modelo só podem exibir os membros.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para executar esse procedimento:  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, veja [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
-   O status da versão deve ser **Aberto**.  
  
-   Você deve ter permissão para acessar a área funcional Gerenciamento de Versões. Para obter mais informações, consulte [Permissões de área funcional &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md).  
  
### <a name="to-lock-a-version"></a>Para bloquear uma versão  
  
1.  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], clique em **Gerenciamento de Versões**.  
  
2.  Na página **Gerenciar Versões** , selecione a linha da versão que você deseja bloquear.  
  
3.  Clique em **Bloquear**.  
  
4.  Na caixa de diálogo de confirmação, clique em **OK**.  
  
## <a name="next-steps"></a>Próximas etapas  
  
-   [Validar uma versão em relação a regras de negócio &#40; Master Data Services &#41;](../master-data-services/validate-a-version-against-business-rules-master-data-services.md)  
  
-   [Confirmar uma versão &#40; Master Data Services &#41;](../master-data-services/commit-a-version-master-data-services.md)  
  
## <a name="see-also"></a>Consulte também  
 [Versões &#40; Master Data Services &#41;](../master-data-services/versions-master-data-services.md)   
 [Desbloquear uma versão &#40; Master Data Services &#41;](../master-data-services/unlock-a-version-master-data-services.md)  
  
  
