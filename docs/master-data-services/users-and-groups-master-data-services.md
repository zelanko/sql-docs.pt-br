---
title: Usuários e Grupos
description: Descubra como conceder acesso ao aplicativo Web Master Data Manager. Um usuário deve ter uma conta adequada.
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
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
ms.openlocfilehash: 0136c2fe08e59169eda2b41a0557b7fd66c3e437
ms.sourcegitcommit: 6be9a0ff0717f412ece7f8ede07ef01f66ea2061
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "92258055"
---
# <a name="users-and-groups-master-data-services"></a>Usuários e grupos (Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  Para acessar o aplicativo Web do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , o usuário deve ter uma conta de domínio do Windows ou uma conta no computador servidor em que o [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] está instalado. Para conceder acesso ao [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , você pode:  
  
-   Adicionar a conta de usuário a um domínio ou grupo local e adicionar o grupo à lista de grupos no [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)].  
  
-   Adicionar a conta de usuário à lista de usuários no [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)].  
  
    > [!NOTE]  
    >  Quando um usuário pertence a um grupo que tem acesso ao [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], o nome do usuário é adicionado automaticamente à lista de usuários na primeira vez que ele acessa o [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] ou o MDS [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)].  
  
 Para executar qualquer ação na área funcional **Explorer** da interface do usuário, o grupo ou usuário deverá ter recebido acesso à área funcional **Explorer** e permissão aos objetos de modelo.  
  
 Se um usuário ou grupo precisar de acesso a outras áreas funcionais, deverá ser atribuído ao usuário ou grupo acesso à área funcional específica.  
  
## <a name="best-practice"></a>Melhor prática  
 Para simplificar a administração, crie grupos e atribua cada permissão de grupo para áreas funcionais e objetos modelo. Em seguida, você pode adicionar e remover usuários dos grupos sem acessar a interface do usuário do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] .  
  
 Não atribua permissões adicionais a um usuário individual e não inclua um usuário em vários grupos que têm acesso ao [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]. Além disso, não use permissões de membro de hierarquia a menos que você deseje que um grupo tenha acesso limitado a membros específicos.  
  
## <a name="see-also"></a>Consulte Também  
 [Adicionar um usuário &#40;Master Data Services&#41;](../master-data-services/add-a-user-master-data-services.md)   
 [Adicionar um grupo &#40;Master Data Services&#41;](../master-data-services/add-a-group-master-data-services.md)   
 [Excluir usuários ou grupos &#40;Master Data Services&#41;](../master-data-services/delete-users-or-groups-master-data-services.md)   
 [Testar permissões de um usuário &#40;Master Data Services&#41;](../master-data-services/test-a-user-s-permissions-master-data-services.md)  
  
  
