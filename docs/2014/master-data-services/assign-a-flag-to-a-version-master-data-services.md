---
title: Atribuir um sinalizador a uma versão (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- version flags [Master Data Services], assigning flags
- versions [Master Data Services], assigning flags
ms.assetid: 6629ec7e-32e7-4a1e-8b31-eb43c5923766
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: b4a6c9c8d24211476d6f0e520da991c239ba7d24
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62926229"
---
# <a name="assign-a-flag-to-a-version-master-data-services"></a>Atribuir um sinalizador a uma versão (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], atribua um sinalizador para uma versão para indicar a versão que usuários ou sistemas de assinatura deveriam usar.  
  
> [!NOTE]  
>  Sinalizadores de versão podem ser atribuídos a apenas uma versão de cada vez. Se você atribuir um sinalizador que já esteja atribuído a outra versão, o sinalizador será movido para a versão selecionada.  
  
## <a name="prerequisites"></a>Prerequisites  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional **Gerenciamento de Versões** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, veja [Administradores &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
-   Você deveria ter criado um sinalizador de versão para atribuir. Para obter mais informações, consulte [Criar um sinalizador de versão &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-version-flag-master-data-services.md).  
  
### <a name="to-assign-a-flag-to-a-version"></a>Para atribuir um sinalizador a uma versão  
  
1.  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], clique em **Gerenciamento de Versões**.  
  
2.  Na página **Gerenciar Versões** , na linha da versão à qual você deseja atribuir um sinalizador, clique duas vezes na célula na coluna **Sinalizador** .  
  
3.  Selecione na lista os sinalizadores que você quer atribuir.  
  
    > [!NOTE]  
    >  Se o sinalizador desejado não estiver disponível, talvez ele só esteja disponível para versões **Confirmadas** . Para confirmar, vá para a página **Gerenciar Sinalizadores de Versão** e exiba o campo **Somente Versões Confirmadas** do sinalizador.  
  
4.  Pressione ENTER para salvar a alteração.  
  
## <a name="see-also"></a>Consulte também  
 [Criar um sinalizador de versão &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-version-flag-master-data-services.md)   
 [Versões &#40;Master Data Services&#41;](../../2014/master-data-services/versions-master-data-services.md)  
  
  
