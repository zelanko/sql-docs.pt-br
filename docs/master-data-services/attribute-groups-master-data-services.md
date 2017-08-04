---
title: Atributo grupos (Master Data Services) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- attribute groups [Master Data Services]
- attribute groups [Master Data Services], about attribute groups
ms.assetid: 648b3d0b-e15a-45f9-8292-3a54a072e62c
caps.latest.revision: 10
author: sabotta
ms.author: carlasab
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: b5c90f2a2df358af81f563f5740450ba130d24e5
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="attribute-groups-master-data-services"></a>Grupos de atributos (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], os grupos de atributos ajudam organizar atributos em uma entidade. Quando uma entidade tem muitos atributos, os grupos de atributos melhoram a maneira como uma entidade é exibida no aplicativo Web do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] .  
  
## <a name="how-attribute-groups-change-the-display"></a>Como os grupos de atributos alteram a exibição  
 Os grupos de atributos são exibidos como guias acima da grade na área funcional **Gerenciador** do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)].  
  
 Quando uma entidade com um grande número de atributos é exibida em uma grade no **Gerenciador**, é necessário rolar para a direita para exibir todos os atributos. Para impedir esse deslocamento, você pode criar grupos de atributos.  
  
-   Os grupos de atributos sempre incluem os atributos Name e Code.  
  
-   Cada atributo de uma entidade pode pertencer a um ou mais grupos de atributos.  
  
-   Todos os atributos são incluídos automaticamente na guia **Todos os Atributos** no **Gerenciador**.  
  
-   Não é possível ocultar a guia **Todos os Atributos** .  
  
 Os grupos de atributos são adminitrados na área funcional **Administração do Sistema** do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)].  
  
## <a name="show-or-hide-attribute-groups"></a>Mostrar ou ocultar grupos de atributos  
 Quando você criar um grupo de atributos, ele será ocultado automaticamente de todos os usuários, exceto daquele que o criou. Para obter mais informações sobre como tornar o grupo visível, consulte [Make an Attribute Group Visible to Users &#40;Master Data Services&#41;](../master-data-services/make-an-attribute-group-visible-to-users-master-data-services.md).  
  
 Se você desejar ocultar um atributo específico em um grupo, poderá atribuir a permissão **Negar** ao atributo. Para obter mais informações, consulte [permissões de folha &#40; Master Data Services &#41; ](../master-data-services/leaf-permissions-master-data-services.md).  
  
## <a name="related-tasks"></a>Tarefas relacionadas  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Criar um novo grupo de atributos e adicionar atributos a ele.|[Criar um grupo de atributos &#40; Master Data Services &#41;](../master-data-services/create-an-attribute-group-master-data-services.md)|  
|Tornar um grupo de atributos visível para os usuários.|[Tornar um grupo de atributos visível para usuários &#40; Master Data Services &#41;](../master-data-services/make-an-attribute-group-visible-to-users-master-data-services.md)|  
|Alterar o nome de um grupo de atributos existente.|[Alterar um nome de grupo de atributos &#40; Master Data Services &#41;](../master-data-services/change-an-attribute-group-name-master-data-services.md)|  
|Excluir um grupo de atributos existente.|[Excluir um grupo de atributos &#40; Master Data Services &#41;](../master-data-services/delete-an-attribute-group-master-data-services.md)|  
  
## <a name="related-content"></a>Conteúdo relacionado  
  
-   [Atributos &#40; Master Data Services &#41;](../master-data-services/attributes-master-data-services.md)  
  
  
