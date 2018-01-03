---
title: Alterar a ordem dos atributos | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: non-specific
ms.reviewer: 
ms.suite: sql
ms.technology: master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 835a032c-e37c-4f35-8ab0-5e4ae25c2e9b
caps.latest.revision: "5"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4e4640bf9b937c4ad513fa568d9c39b65526b0e6
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="change-the-order-of-attributes"></a>Alterar a ordem dos atributos
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], você pode alterar a ordem dos atributos.  
  
## <a name="prerequisites"></a>Prerequisites  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional **Administração do Sistema** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, veja [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
### <a name="to-change-the-order-of-an-attribute"></a>Para alterar a ordem de um atributo  
  
1.  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], clique em **Administração do Sistema**.  
  
2.  Na página **Gerenciar Modelo** , selecione um modelo na grade e clique em **Entidades**.  
  
3.  Na página **Gerenciar Entidade** , selecione a linha da entidade para a qual deseja criar um atributo.  
  
4.  Clique em **Atributos**.  
  
5.  Na página **Gerenciar atributos** , realize um dos procedimentos a seguir.  
  
    -   Se o atributo for para membros folha, selecione **Folha** na caixa de listagem **Tipos de Membro** .  
  
    -   Se o atributo for para membros consolidados, selecione **Consolidado** na caixa de listagem **Tipos de Membro** .  
  
    -   Se o atributo for para coleções, selecione **Coleção** na caixa de listagem **Tipos de Membro** .  
  
6.  Selecione a linha para o atributo cuja ordem você deseja alterar.  
  
    > [!NOTE]  
    >  Não é possível alterar a ordem dos os atributos Name e Code.  
  
7.  Clique em **Mover para Cima** ou **Mover para Baixo**.  
  
## <a name="see-also"></a>Consulte Também  
 [Atributos &#40;Master Data Services&#41;](../master-data-services/attributes-master-data-services.md)  
  
  
