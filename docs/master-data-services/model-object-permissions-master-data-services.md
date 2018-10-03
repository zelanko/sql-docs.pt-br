---
title: Permissões de objeto de modelo (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
helpviewer_keywords:
- permissions [Master Data Services], model objects
- models [Master Data Services], object permissions
ms.assetid: fab6335b-4cae-47de-ae7c-6c4743e0680f
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 9d2289a199ec54eacb42a5fce175f91872ab8133
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47848847"
---
# <a name="model-object-permissions-master-data-services"></a>Permissões de objeto de modelo (Serviços de Dados Mestre)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  As permissões do objeto de modelo são obrigatórias. Elas determinam os atributos que um usuário pode acessar na área funcional **Explorer** da interface do usuário.  
  
 Por exemplo, se você atribuir uma permissão **Atualizar** de usuário à entidade Produto, o usuário poderá atualizar todos os atributos dessa entidade. Se você atribuir a permissão **Atualizar** a um único atributo, o usuário só poderá atualizar esse atributo.  
  
 Para determinar a segurança atribuída em cada valor de atributo individual, permissões de objeto modelo são combinadas com permissões de membro de hierarquia, que determinam os membros que um usuário pode acessar.  
  
 Para conceder a um usuário acesso a uma área funcional, que não seja o **Explorer**, esse usuário precisa ser o administrador de modelo, o que também envolve a atribuição de permissões de Administrador no objeto de modelo. Para obter mais informações, veja [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
 As permissões de objeto de modelo são atribuídas na interface do usuário do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], na área funcional **Permissões para Usuário e Grupo** da guia **Modelos**. Nesta guia, o modelo é representado como uma estrutura de árvore. Quando você atribui uma permissão a um objeto na árvore, todos os objetos abaixo herdam a permissão. Você pode substituir essa herança atribuindo permissões aos objetos individuais.  
  
 Você pode atribuir uma combinação permissões Ler, Criar, Atualizar e Excluir ou Negar para objetos de modelo. Se você não atribuir nenhuma permissão na guia **Modelos** , o usuário não poderá exibir modelos nem dados no [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)].  
  
## <a name="best-practice"></a>Prática recomendada  
 Em geral, é necessário atribuir a permissão **ALL** ao objeto modelo e atribuir explicitamente a permissão aos objetos subjacentes.  
  
## <a name="external-resources"></a>Recursos externos  
 Postagem do blog, [Aprimoramentos de Segurança](http://go.microsoft.com/fwlink/p/?LinkId=615376), em msdn.com.  
  
## <a name="see-also"></a>Consulte Também  
 [Atribuir permissões de objeto de modelo &#40;Master Data Services&#41;](../master-data-services/assign-model-object-permissions-master-data-services.md)   
 [Permissões de modelo &#40;Master Data Services&#41;](../master-data-services/model-permissions-master-data-services.md)   
 [Permissões de área funcional &#40;Master Data Services&#41;](../master-data-services/functional-area-permissions-master-data-services.md)   
 [Permissões de membro de hierarquia &#40;Master Data Services&#41;](../master-data-services/hierarchy-member-permissions-master-data-services.md)   
 [Como as permissões são determinadas &#40;Master Data Services&#41;](../master-data-services/how-permissions-are-determined-master-data-services.md)  
  
  
