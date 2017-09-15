---
title: "Tornar um grupo de atributos visível para os usuários (Master Data Services) | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b2f6cc27-dbc9-4f3f-961e-e81e76375248
caps.latest.revision: 6
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: e3922c3ad81de37e73f08bd840def40146c8bf12
ms.contentlocale: pt-br
ms.lasthandoff: 09/07/2017

---
# <a name="make-an-attribute-group-visible-to-users-master-data-services"></a>Tornar um grupo de atributos visível para os usuários (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], torne um grupo de atributos visível para usuários ou grupos quando você desejar que os usuários tenham guias acima da grade na área funcional do **Explorer** .  
  
 Quando você criar um grupo de atributos, ele será ocultado automaticamente de todos os usuários, exceto daquele que o criou.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional **Administração do Sistema** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, veja [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
-   Pelo menos um grupo de atributos deve existir. Para obter mais informações, veja [Criar um grupo de atributos &#40;Master Data Services&#41;](../master-data-services/create-an-attribute-group-master-data-services.md).  
  
### <a name="to-make-an-attribute-group-visible-to-users"></a>Para tornar um grupo de atributos visível para usuários  
  
1.  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], clique em **Administração do Sistema**.  
  
2.  Na página **Gerenciar Modelo** , escolha um modelo na grade e clique em **Entidades**.  
  
3.  Na página **Gerenciar Entidade** , na grade, selecione a linha para a entidade que você deseja editar o grupo de atributos.  
  
4.  Clique em **Grupos de Atributos**.  
  
5.  Na página **Gerenciar Grupos de Atributos** , selecione o tipo de membro na caixa de listagem suspensa **Tipos de Membro** para expandir **Folha**, **Consolidado** ou **Coleção**, dependendo do tipo de grupo que você deseja tornar visível.  
  
6.  Selecione o grupo de atributos que você deseja editar da grade e clique em **Editar**.  
  
7.  Clique em um usuário ou grupo na caixa **Disponível** e clique na seta **Adicionar** . Para adicionar tudo, clique na seta **Adicionar Tudo** .  
  
8.  Clique em **Salvar**.  
  
## <a name="see-also"></a>Consulte também  
 [Grupos de atributos &#40;Master Data Services&#41;](../master-data-services/attribute-groups-master-data-services.md)   
 [Criar um grupo de atributos &#40;Master Data Services&#41;](../master-data-services/create-an-attribute-group-master-data-services.md)  
  
  
