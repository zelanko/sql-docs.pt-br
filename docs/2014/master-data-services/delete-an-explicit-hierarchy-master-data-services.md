---
title: Excluir uma hierarquia explícita (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- explicit hierarchies, deleting
- deleting explicit hierarchies [Master Data Services]
ms.assetid: 4ce177b0-9884-47a2-9cea-212e845dd762
caps.latest.revision: 4
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 08770818215b1055f2f5a015a696979bcea74f69
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36005899"
---
# <a name="delete-an-explicit-hierarchy-master-data-services"></a>Excluir uma hierarquia explícita (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], exclua uma hierarquia explícita quando você já não precisar mais dela.  
  
> [!WARNING]  
>  Quando você excluir uma hierarquia explícita, todos os membros consolidados na hierarquia também serão excluídos. Se você excluir todas as hierarquias explícitas de uma entidade, serão excluídas também todas as coleções na entidade, que deixará de estar habilitada para hierarquias explícitas e coleções.  
  
## <a name="prerequisites"></a>Prerequisites  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional **Administração do Sistema** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, veja [Administrators &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
### <a name="to-delete-an-explicit-hierarchy"></a>Para excluir uma hierarquia explícita  
  
1.  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], clique em **Administração do Sistema**.  
  
2.  Na página **Exibição de Modelos** , na barra de menus, aponte para **Gerenciar** e clique em **Entidades**.  
  
3.  Na página **Manutenção da Entidade** , na lista **Modelo** , selecione um modelo.  
  
4.  Selecione a linha da entidade que contém a hierarquia explícita que você deseja excluir.  
  
5.  Clique em **Editar entidade selecionada**.  
  
6.  No **Editar entidade** página, o **hierarquias explícitas** painel, clique na hierarquia explícita que você deseja excluir.  
  
7.  Clique em **excluir hierarquia selecionada**.  
  
8.  Na caixa de diálogo de confirmação, clique em **OK**.  
  
9. Na caixa de diálogo de confirmação adicional, clique em **OK**.  
  
## <a name="see-also"></a>Consulte também  
 [Criar uma hierarquia explícita &#40;Master Data Services&#41;](../../2014/master-data-services/create-an-explicit-hierarchy-master-data-services.md)   
 [Hierarquias explícitas &#40;Master Data Services&#41;](../../2014/master-data-services/explicit-hierarchies-master-data-services.md)  
  
  