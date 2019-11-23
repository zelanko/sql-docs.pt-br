---
title: Atribuir permissões de objeto modelo
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- models [Master Data Services], assigning object permissions
- permissions [Master Data Services], assigning model object permissions
ms.assetid: 4b80148d-2318-415c-9479-28c240e48bcd
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: a6c1dbc6be8ba8ddde53ea1ccdfa97fe7992a4b5
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73728743"
---
# <a name="assign-model-object-permissions-master-data-services"></a>Atribuir permissões de objeto modelo (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], atribua permissões a objetos modelo quando você precisar fornecer a um usuário ou grupo o acesso aos dados na área funcional **Explorer** do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], ou quando precisar tornar um usuário ou grupo um administrador.  
  
> [!NOTE]  
>  Quando você atribui permissão a um modelo, a permissão a todos os outros modelos é negada implicitamente. Se você não atribuir permissões a objetos de modelo, o usuário ou grupo não poderá acessar nenhum dado no **Explorer**.  
  
## <a name="prerequisites"></a>Prerequisites  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional **Permissões de Usuário e Grupo** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, veja [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
### <a name="to-assign-model-object-permissions"></a>Para atribuir permissões de objeto de modelo  
  
1.  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], clique em **Permissões de Usuário e Grupo**.  
  
2.  Na página **Usuários** ou **Grupos** , selecione a linha do usuário ou grupo que deseja editar.  
  
3.  Clique em **Editar usuário selecionado**.  
  
4.  Clique na guia **Modelos** .  
  
5.  Opcionalmente, selecione um modelo na lista **Modelo** .  
  
6.  Clique em **Editar**.  
  
7.  Expanda a árvore e clique no objeto de modelo ao qual deseja atribuir permissões.  
  
8.  No menu, selecione uma combinação de Ler, Criar, Atualizar e Excluir ou Negar.  
  
9. No nível de modelo superior, selecione **Administrador** se precisar transformar um usuário em administrador de modelo.  
  
10. Clique em **Salvar**.  
  
## <a name="next-steps"></a>Next Steps  
  
-   (Opcional) [Atribuir permissões de membro de hierarquia &#40;Master Data Services&#41;](../master-data-services/assign-hierarchy-member-permissions-master-data-services.md)  
  
## <a name="see-also"></a>Consulte também  
 [Excluir permissões de objeto de modelo &#40;Master Data Services&#41;](../master-data-services/delete-model-object-permissions-master-data-services.md)   
 [Permissões de objeto de modelo &#40;Master Data Services&#41;](../master-data-services/model-object-permissions-master-data-services.md)   
 [Criar um administrador de modelo &#40;Master Data Services&#41;](../master-data-services/create-a-model-administrator-master-data-services.md)  
  
  
