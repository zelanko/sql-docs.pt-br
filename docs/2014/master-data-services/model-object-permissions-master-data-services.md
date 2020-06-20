---
title: Permissões de objeto de modelo (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- permissions [Master Data Services], model objects
- models [Master Data Services], object permissions
ms.assetid: fab6335b-4cae-47de-ae7c-6c4743e0680f
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 754920cac0a832ac5ae1ff8959e710815d68fd70
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84971186"
---
# <a name="model-object-permissions-master-data-services"></a>Permissões de objeto de modelo (Serviços de Dados Mestre)
  As permissões do objeto de modelo são obrigatórias. Elas determinam os atributos que um usuário pode acessar na área funcional **Explorer** da interface do usuário.  
  
 Por exemplo, se você atribuir uma permissão **Atualizar** de usuário à entidade Produto, o usuário poderá atualizar todos os atributos dessa entidade. Se você atribuir a permissão **Atualizar** a um único atributo, o usuário só poderá atualizar esse atributo.  
  
 Para determinar a segurança atribuída em cada valor de atributo individual, permissões de objeto modelo são combinadas com permissões de membro de hierarquia, que determinam os membros que um usuário pode acessar.  
  
 Para conceder a um usuário acesso a uma área funcional diferente do **Explorer**, o usuário deve ser um administrador de modelo, que também envolve a atribuição de permissões de objeto de modelo. Para obter mais informações, consulte [administradores &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
 As permissões de objeto de modelo são atribuídas na [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] interface do usuário, na área funcional **permissões de usuário e grupo** na guia **modelos** . Nessa guia, o modelo é representado como uma estrutura de árvore. Quando você atribui uma permissão a um objeto na árvore, todos os objetos abaixo herdam a permissão. Você pode substituir essa herança atribuindo permissões aos objetos individuais.  
  
 Você pode atribuir permissão **somente leitura**, **Atualizar**ou **negar** a objetos de modelo. Se você não atribuir nenhuma permissão na guia **Modelos** , o usuário não poderá exibir modelos nem dados no [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)].  
  
## <a name="best-practice"></a>Melhor prática  
 Em geral, você deve atribuir a permissão **Atualizar** ao objeto de modelo e atribuir explicitamente permissão a objetos abaixo. Se você não atribuir permissão a objetos subjacentes, as permissões serão herdadas e o usuário será um administrador.  
  
## <a name="see-also"></a>Consulte Também  
 [Atribuir permissões de objeto de modelo &#40;Master Data Services&#41;](../../2014/master-data-services/assign-model-object-permissions-master-data-services.md)   
 [Permissões de modelo &#40;Master Data Services&#41;](../../2014/master-data-services/model-permissions-master-data-services.md)   
 [Permissões de área funcional &#40;Master Data Services&#41;](../../2014/master-data-services/functional-area-permissions-master-data-services.md)   
 [Permissões de membro de hierarquia &#40;Master Data Services&#41;](../../2014/master-data-services/hierarchy-member-permissions-master-data-services.md)   
 [Como as permissões são determinadas &#40;Master Data Services&#41;](../../2014/master-data-services/how-permissions-are-determined-master-data-services.md)  
  
  
