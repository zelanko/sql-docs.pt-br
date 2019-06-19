---
title: Excluir permissões de membro de hierarquia (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- deleting member permissions [Master Data Services]
- members [Master Data Services], deleting permissions
- permissions [Master Data Services], deleting member permissions
ms.assetid: 7f22d5e2-70c1-422c-99c2-e995a47d812a
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 853bc9ce4b2f0432f74e3876f9a6234042fe5b5e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65479511"
---
# <a name="delete-hierarchy-member-permissions-master-data-services"></a>Excluir permissões de membro de hierarquia (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], exclua as permissões do objeto de modelo para remover as atribuições feitas.  
  
## <a name="prerequisites"></a>Prerequisites  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional **Permissões de Usuário e Grupo** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, veja [Administradores &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
### <a name="to-delete-hierarchy-member-permissions"></a>Para excluir permissões de membro de hierarquia  
  
1.  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], clique em **Permissões de Usuário e Grupo**.  
  
2.  Na página **Usuários** ou **Grupos** , selecione a linha do usuário ou grupo que deseja editar.  
  
3.  Clique em **Editar usuário selecionado**.  
  
4.  Clique na guia **Membros da Hierarquia** .  
  
5.  Na lista **Modelo** , selecione um modelo.  
  
6.  Na lista **Versão** , selecione uma versão.  
  
7.  No **resumo de permissões de membro de hierarquia** painel, selecione a linha para a permissão que você deseja excluir.  
  
8.  Clique em **excluir permissão selecionada**.  
  
    > [!NOTE]  
    >  Você não poderá remover uma permissão de um usuário se a permissão for herdada de um grupo. Em vez disso, você deve remover a permissão do grupo.  
  
## <a name="see-also"></a>Consulte também  
 [Permissões de membro de hierarquia &#40;Master Data Services&#41;](../../2014/master-data-services/hierarchy-member-permissions-master-data-services.md)   
 [Atribuir permissões de membro de hierarquia &#40;Master Data Services&#41;](../../2014/master-data-services/assign-hierarchy-member-permissions-master-data-services.md)  
  
  
