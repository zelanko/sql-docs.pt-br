---
title: Excluir usuários ou grupos (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- deleting groups [Master Data Services]
- groups [Master Data Services], deleting
- users [Master Data Services], deleting
- deleting users [Master Data Services]
ms.assetid: 0bbf9d2c-b826-48bb-8aa9-9905db6e717f
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 61044c03428fc3713d78dc569248cc823e986286
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52821858"
---
# <a name="delete-users-or-groups-master-data-services"></a>Excluir usuários ou grupos (Master Data Services)
  Exclua usuários ou grupos quando não desejar mais que eles acessem o [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)].  
  
 Observe o seguinte comportamento ao excluir usuários e grupos:  
  
-   Se você excluir um usuário que é membro de um grupo com acesso ao [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], ele ainda poderá acessar o [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] até que você o remova do Active Directory ou do grupo local.  
  
-   Se você excluir um grupo, todos os usuários do grupo que acessaram o [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] serão exibidos na lista **Usuários** até que você os exclua.  
  
-   As alterações na segurança não são propagadas no MDS [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)] durante 20 minutos.  
  
## <a name="prerequisites"></a>Prerequisites  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional **Permissões de Usuário e Grupo** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, veja [Administradores &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
### <a name="to-delete-users-or-groups"></a>Para excluir usuários ou grupos  
  
1.  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], clique em **Permissões de Usuário e Grupo**.  
  
2.  Para excluir um usuário, permaneça na página **Usuários** . Para excluir um grupo, na barra de menus, clique em **Gerenciar Grupos**.  
  
3.  Na grade, selecione a linha correspondente ao usuário ou grupo que você deseja excluir.  
  
4.  Clique em **Excluir usuário selecionado** ou **Excluir grupo selecionado**.  
  
5.  Na caixa de diálogo de confirmação, clique em **OK**.  
  
## <a name="see-also"></a>Consulte também  
 [Segurança &#40;Master Data Services&#41;](../../2014/master-data-services/security-master-data-services.md)  
  
  
