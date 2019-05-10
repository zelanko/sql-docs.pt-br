---
title: Bloquear uma versão (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- versions [Master Data Services], locking
- locking versions [Master Data Services]
ms.assetid: 7bb62a84-12d8-4b29-9b6e-6aa25410618e
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 4c2478cfa5753c094284f44c13cf0037bf927a5a
ms.sourcegitcommit: 5748d710960a1e3b8bb003d561ff7ceb56202ddb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65488347"
---
# <a name="lock-a-version-master-data-services"></a>Bloquear uma versão (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], bloqueie uma versão de um modelo para evitar alterações nos membros do modelo e em seus atributos.  
  
> [!NOTE]  
>  Quando uma versão estiver bloqueada, os administradores do modelo poderão continuar adicionando, editando e removendo membros. Outros usuários com permissão para o modelo só podem exibir os membros.  
  
## <a name="prerequisites"></a>Prerequisites  
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
  
-   [Validar uma versão em relação a regras de negócio &#40;Master Data Services&#41;](../master-data-services/validate-a-version-against-business-rules-master-data-services.md)  
  
-   [Confirmar uma versão &#40;Master Data Services&#41;](../master-data-services/commit-a-version-master-data-services.md)  
  
## <a name="see-also"></a>Consulte também  
 [Versões &#40;Master Data Services&#41;](../master-data-services/versions-master-data-services.md)   
 [Desbloquear uma versão &#40;Master Data Services&#41;](../master-data-services/unlock-a-version-master-data-services.md)  
  
  
