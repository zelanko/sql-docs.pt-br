---
title: Grupos de atributos (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- attribute groups [Master Data Services]
- attribute groups [Master Data Services], about attribute groups
ms.assetid: 648b3d0b-e15a-45f9-8292-3a54a072e62c
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 73b2409f8e3b5b58be15351e05abd92dfc94ac8b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62877373"
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
 Quando você criar um grupo de atributos, ele será ocultado automaticamente de todos os usuários, exceto daquele que o criou. Para obter mais informações sobre como tornar o grupo visível, consulte [Make an Attribute Group Visible to Users &#40;Master Data Services&#41;](make-an-attribute-group-visible-to-users-master-data-services.md).  
  
 Se você desejar ocultar um atributo específico em um grupo, poderá atribuir a permissão **Negar** ao atributo. Para obter mais informações, consulte [Permissões de folha &#40;Master Data Services&#41;](../../2014/master-data-services/leaf-permissions-master-data-services.md) ou [Permissões consolidadas &#40;Master Data Services&#41;](../../2014/master-data-services/consolidated-permissions-master-data-services.md).  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Criar um novo grupo de atributos e adicionar atributos a ele.|[Criar um grupo de atributos &#40;Master Data Services&#41;](../../2014/master-data-services/create-an-attribute-group-master-data-services.md)|  
|Tornar um grupo de atributos visível para os usuários.|[Tornar um grupo de atributos visível para os usuários &#40;Master Data Services&#41;](make-an-attribute-group-visible-to-users-master-data-services.md)|  
|Alterar o nome de um grupo de atributos existente.|[Alterar o nome de um grupo de atributos &#40;Master Data Services&#41;](../../2014/master-data-services/change-an-attribute-group-name-master-data-services.md)|  
|Excluir um grupo de atributos existente.|[Excluir um grupo de atributos &#40;Master Data Services&#41;](../../2014/master-data-services/delete-an-attribute-group-master-data-services.md)|  
  
## <a name="related-content"></a>Conteúdo relacionado  
  
-   [Atributos &#40;Master Data Services&#41;](../../2014/master-data-services/attributes-master-data-services.md)  
  
  
