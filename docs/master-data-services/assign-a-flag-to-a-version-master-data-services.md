---
title: Atribuir um sinalizador a uma versão
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- version flags [Master Data Services], assigning flags
- versions [Master Data Services], assigning flags
ms.assetid: 6629ec7e-32e7-4a1e-8b31-eb43c5923766
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 4e8f69d473ff15be3105c8dcef5f51edf30f4302
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73729784"
---
# <a name="assign-a-flag-to-a-version-master-data-services"></a>Atribuir um sinalizador a uma versão (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], atribua um sinalizador para uma versão para indicar a versão que usuários ou sistemas de assinatura deveriam usar.  
  
> [!NOTE]  
>  Sinalizadores de versão podem ser atribuídos a apenas uma versão de cada vez. Se você atribuir um sinalizador que já esteja atribuído a outra versão, o sinalizador será movido para a versão selecionada.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional **Gerenciamento de Versões** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, veja [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
-   Você deveria ter criado um sinalizador de versão para atribuir. Para obter mais informações, veja [Create a Version Flag &#40;Master Data Services&#41;](../master-data-services/create-a-version-flag-master-data-services.md).  
  
-   Você deve ter permissão para acessar a área funcional Gerenciamento de Versões. Para obter mais informações, consulte [Permissões de área funcional &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md).  
  
### <a name="to-assign-a-flag-to-a-version"></a>Para atribuir um sinalizador a uma versão  
  
1.  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], clique em **Gerenciamento de Versões**.  
  
2.  Na página **Gerenciar Versões** , na linha da versão à qual você deseja atribuir um sinalizador, clique duas vezes na célula na coluna **Sinalizador** .  
  
3.  Selecione na lista os sinalizadores que você quer atribuir.  
  
    > [!NOTE]  
    >  Se o sinalizador desejado não estiver disponível, talvez ele só esteja disponível para versões **Confirmadas** . Para confirmar, vá para a página **Gerenciar Sinalizadores de Versão** e exiba o campo **Somente Versões Confirmadas** do sinalizador.  
  
4.  Pressione ENTER para salvar a alteração.  
  
## <a name="see-also"></a>Consulte também  
 [Criar um sinalizador de versão &#40;Master Data Services&#41;](../master-data-services/create-a-version-flag-master-data-services.md)   
 [Versões &#40;Master Data Services&#41;](../master-data-services/versions-master-data-services.md)  
  
  
