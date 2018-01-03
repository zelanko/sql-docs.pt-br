---
title: "Criar um sinalizador de versão (Master Data Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: non-specific
ms.reviewer: 
ms.suite: sql
ms.technology: master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- creating version flags [Master Data Services]
- version flags [Master Data Services], creating
- versions [Master Data Services], creating flags
ms.assetid: 3067e1e3-05b7-4f11-9206-c612ef4e7e42
caps.latest.revision: "7"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6b309c06b5bdb7904b74127189d3efb97cd147b8
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="create-a-version-flag-master-data-services"></a>Criar um sinalizador de versão (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], crie um sinalizador de versão a ser atribuído a uma versão. O sinalizador pode indicar a versão que os usuários ou sistemas de assinatura devem usar.  
  
## <a name="prerequisites"></a>Prerequisites  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional **Gerenciamento de Versões** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, veja [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
-   Você deve ter permissão para acessar a área funcional Gerenciamento de Versões. Para obter mais informações, consulte [Permissões de área funcional &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md).  
  
### <a name="to-create-a-version-flag"></a>Para criar um sinalizador de versão  
  
1.  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], clique em **Gerenciamento de Versões**.  
  
2.  Na página **Gerenciar Versões** , na barra de menus, aponte para **Gerenciar** e clique em **Sinalizadores**.  
  
3.  Na página **Gerenciar Sinalizadores de Versão** , no campo **Modelo** , selecione o modelo para o qual você deseja criar um sinalizador.  
  
4.  Clique em **Adicionar**.  
  
5.  Na caixa **Nome** , digite um nome.  
  
6.  Na caixa **Descrição** , digite uma descrição.  
  
7.  No campo **Somente Versões Confirmadas** , selecione **True** para indicar que o sinalizador pode ser atribuído a versões apenas com um status de **Confirmado** . Selecione **False** para indicar que o sinalizador pode ser atribuído a versões com qualquer status.  
  
8.  Clique em **Salvar**.  
  
## <a name="next-steps"></a>Next Steps  
  
-   [Atribuir um sinalizador a uma versão &#40;Master Data Services&#41;](../master-data-services/assign-a-flag-to-a-version-master-data-services.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Versões &#40;Master Data Services&#41;](../master-data-services/versions-master-data-services.md)   
 [Alterar o nome de um sinalizador de versão &#40;Master Data Services&#41;](../master-data-services/change-a-version-flag-name-master-data-services.md)  
  
  
