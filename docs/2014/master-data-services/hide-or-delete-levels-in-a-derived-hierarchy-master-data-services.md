---
title: Ocultar ou excluir níveis em uma hierarquia derivada (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- derived hierarchies, hiding levels
- derived hierarchies, deleting levels
ms.assetid: e00582b9-9415-4b66-b4a7-9f590d83875f
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 3bc04f53a8ea80a54b4e0810aa9378f1af4dd2e1
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84971436"
---
# <a name="hide-or-delete-levels-in-a-derived-hierarchy-master-data-services"></a>Ocultar ou excluir níveis em uma hierarquia derivada (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], oculte um nível em uma hierarquia derivada quando você precisar agrupar o nível, mas não for necessário mostrar o nível. Exclua um nível quando você não quiser usá-lo para agrupamento.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional **Administração do sistema** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, consulte [administradores &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
### <a name="to-hide-or-delete-levels-in-a-derived-hierarchy"></a>Para ocultar ou excluir níveis em uma hierarquia derivada  
  
1.  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], clique em **Administração do Sistema**.  
  
2.  Na página **exibição de modelo** , na barra de menus, aponte para **gerenciar** e clique em **hierarquias derivadas**.  
  
3.  Na página **Manutenção da Hierarquia Derivada** , na lista **Modelo** , selecione um modelo.  
  
4.  Selecione a linha da hierarquia derivada que você deseja editar.  
  
5.  Clique em **Editar hierarquia derivada selecionada**.  
  
6.  No painel **Níveis Atuais** :  
  
    -   Para ocultar um nível, clique em um nível sem ser o superior ou o inferior. Na lista **Visível** , selecione **Não**. Em seguida, clique em **Salvar item de hierarquia selecionado**.  
  
    -   Para excluir o nível superior, clique em **Excluir item de hierarquia selecionado**. Na caixa de diálogo de confirmação, clique em **OK**. Somente é possível excluir o nível superior.  
  
## <a name="see-also"></a>Consulte Também  
 [Mover membros dentro de uma hierarquia &#40;Master Data Services&#41;](../../2014/master-data-services/move-members-within-a-hierarchy-master-data-services.md)   
 [Hierarquias derivadas &#40;Master Data Services&#41;](../../2014/master-data-services/derived-hierarchies-master-data-services.md)  
  
  
