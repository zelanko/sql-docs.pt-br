---
title: Confirmar uma versão
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- committing versions [Master Data Services]
- versions [Master Data Services], committing
ms.assetid: 6b967a39-b333-4b84-9e5f-4fb07e156826
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 0fa359de1daa844fbcce073b0c67efdd5f721b37
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "73728594"
---
# <a name="commit-a-version-master-data-services"></a>Confirmar uma versão (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], confirme uma versão de um modelo para evitar alterações para os membros do modelo e seus atributos. As versões confirmadas não podem ser desbloqueadas.  
  
## <a name="prerequisites"></a>Prerequisites  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional **Gerenciamento de Versões** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, veja [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
-   O status da versão deverá ser **Bloqueado**. Para obter mais informações, veja [Bloquear uma versão &#40;Master Data Services&#41;](../master-data-services/lock-a-version-master-data-services.md).  
  
-   Todos os membros devem ter validado com êxito.  
  
-   Você deve ter permissão para acessar a área funcional Gerenciamento de Versões. Para obter mais informações, consulte [Permissões de área funcional &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md).  
  
### <a name="to-commit-a-version"></a>Para confirmar uma versão  
  
1.  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], clique em **Gerenciamento de Versões**.  
  
2.  Na página **Gerenciar Versões** , na barra de menus, clique em **Validar Versão**.  
  
3.  Na página **Validar Versão** , selecione o modelo e a versão que deseja confirmar.  
  
4.  Clique em **Confirmar**.  
  
5.  Na caixa de diálogo de confirmação, clique em **OK**.  
  
## <a name="next-steps"></a>Próximas etapas  
  
-   [Criar um sinalizador de versão &#40;Master Data Services&#41;](../master-data-services/create-a-version-flag-master-data-services.md)  
  
-   [Atribuir um sinalizador a uma versão &#40;Master Data Services&#41;](../master-data-services/assign-a-flag-to-a-version-master-data-services.md)  
  
-   [Copiar uma versão &#40;Master Data Services&#41;](../master-data-services/copy-a-version-master-data-services.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Versões &#40;Master Data Services&#41;](../master-data-services/versions-master-data-services.md)  
  
  
