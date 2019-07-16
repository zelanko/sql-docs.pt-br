---
title: Ocultar ou excluir níveis em uma hierarquia derivada (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- derived hierarchies, hiding levels
- derived hierarchies, deleting levels
ms.assetid: e00582b9-9415-4b66-b4a7-9f590d83875f
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 0b6ce19214332e2a4f2ec85735657e7e55906c44
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67945245"
---
# <a name="hide-or-delete-levels-in-a-derived-hierarchy-master-data-services"></a>Ocultar ou excluir níveis em uma hierarquia derivada (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], oculte um nível em uma hierarquia derivada quando você precisar agrupar o nível, mas não for necessário mostrar o nível. Exclua um nível quando você não quiser usá-lo para agrupamento.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional **Administração do Sistema** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, veja [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
### <a name="to-hide-or-delete-levels-in-a-derived-hierarchy"></a>Para ocultar ou excluir níveis em uma hierarquia derivada  
  
1.  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], clique em **Administração do Sistema**.  
  
2.  Na barra de menus, aponte para **Gerenciar** e clique em **Hierarquias Derivadas**.  
  
3.  Na página **Manutenção da Hierarquia Derivada** , na lista **Modelo** , selecione um modelo.  
  
4.  Selecione a linha da hierarquia derivada que você deseja editar.  
  
5.  Clique em **Editar**.  
  
6.  No painel **Níveis Atuais** :  
  
    -   Para ocultar um nível, clique em um nível sem ser o superior ou o inferior. Na lista **Visível** , selecione **Não**. Em seguida, clique em **Salvar item de hierarquia selecionado**.  
  
    -   Para excluir o nível superior, clique em **Excluir item de hierarquia selecionado**. Na caixa de diálogo de confirmação, clique em **OK**. Somente é possível excluir o nível superior.  
  
## <a name="see-also"></a>Consulte também  
    
 [Hierarquias derivadas &#40;Master Data Services&#41;](../master-data-services/derived-hierarchies-master-data-services.md)  
  
  
