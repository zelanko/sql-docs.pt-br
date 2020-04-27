---
title: Usuários e grupos (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- users [Master Data Services]
- groups [Master Data Services]
- users [Master Data Services], about users
- groups [Master Data Services], about groups
ms.assetid: ed08dd2d-248e-4b68-91d4-e9961cb50eed
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 58373531871a5db8ff859280de52cbe21562bfb5
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "65478622"
---
# <a name="users-and-groups-master-data-services"></a>Usuários e grupos (Master Data Services)
  Para acessar o aplicativo Web do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , o usuário deve ter uma conta de domínio do Windows ou uma conta no computador servidor em que o [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] está instalado. Para conceder acesso ao [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , você pode:  
  
-   Adicionar a conta de usuário a um domínio ou grupo local e adicionar o grupo à lista de grupos no [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)].  
  
-   Adicionar a conta de usuário à lista de usuários no [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)].  
  
    > [!NOTE]  
    >  Quando um usuário pertence a um grupo que tem acesso ao [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], o nome do usuário é adicionado automaticamente à lista de usuários na primeira vez que ele acessa o [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] ou o MDS [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)].  
  
 Para executar qualquer ação na área funcional **Explorer** da interface do usuário, o grupo ou usuário deverá ter recebido acesso à área funcional **Explorer** e permissão aos objetos de modelo.  
  
 Se um usuário ou grupo precisar de acesso a outras áreas funcionais, o usuário ou grupo deverá ser um administrador. Para obter mais informações, consulte [administradores &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
## <a name="best-practice"></a>Melhor prática  
 Para simplificar a administração, crie grupos e atribua cada permissão de grupo para áreas funcionais e objetos modelo. Em seguida, você pode adicionar e remover usuários dos grupos sem acessar a interface do usuário do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] .  
  
 Não atribua permissões adicionais a um usuário individual e não inclua um usuário em vários grupos que têm acesso ao [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]. Além disso, não use permissões de membro de hierarquia a menos que você deseje que um grupo tenha acesso limitado a membros específicos.  
  
## <a name="see-also"></a>Consulte Também  
 [Adicionar um usuário &#40;Master Data Services&#41;](../../2014/master-data-services/add-a-user-master-data-services.md)   
 [Adicionar um grupo &#40;Master Data Services&#41;](../../2014/master-data-services/add-a-group-master-data-services.md)   
 [Excluir usuários ou grupos &#40;Master Data Services&#41;](../../2014/master-data-services/delete-users-or-groups-master-data-services.md)   
 [Testar permissões de um usuário &#40;Master Data Services&#41;](../../2014/master-data-services/test-a-user-s-permissions-master-data-services.md)  
  
  
