---
title: Criar um membro consolidado (Master Data Services) | Microsoft Docs
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
- creating consolidated members [Master Data Services]
- members [Master Data Services], creating consolidated members
- consolidated members [Master Data Services], creating
ms.assetid: 431ab2d2-5517-4372-9980-142b05427c08
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: c56cf77e3b790a6e188be1ebaf1b2e7da04b92b7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36006129"
---
# <a name="create-a-consolidated-member-master-data-services"></a>Criar um membro consolidado (Master Data Services)
  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], crie um membro consolidado quando você desejar um nó pai para uma hierarquia explícita. Os membros consolidados podem ter seus próprios atributos. Eles são usados para agrupamento. Conforme mostrado no exemplo a seguir, os membros consolidados podem ser usados para grupos de contas que têm contas neles.  
  
 ![Membros consolidados de MDS](../../2014/master-data-services/media/mds-consolidated-members.png "membros consolidados do MDS")  
  
## <a name="prerequisites"></a>Prerequisites  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional do **Gerenciador** .  
  
-   Você deve ter, no mínimo, a permissão **Atualizar** para o objeto de modelo consolidado para a entidade a qual você está adicionando um membro.  
  
### <a name="to-create-a-consolidated-member"></a>Para criar um membro consolidado  
  
1.  Na home page do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , na lista **Modelo** , selecione um modelo.  
  
2.  Na lista **Versão** , selecione uma versão.  
  
3.  Clique em **Gerenciador**.  
  
4.  Na barra de menus, aponte para **Hierarquias** e clique no nome da hierarquia à qual você deseja adicionar um membro consolidado.  
  
5.  Acima da grade, selecione a opção **Membros consolidados** ou **Todos os membros consolidados da hierarquia** .  
  
6.  Clique em **Adicionar**.  
  
7.  No painel à direita, preencha os campos.  
  
8.  Opcional. Na caixa **Anotações** , digite um comentário sobre por que o membro foi adicionado. Todos os usuários que têm acesso ao membro podem exibir a anotação.  
  
9. Clique em **OK**.  
  
## <a name="next-steps"></a>Próximas etapas  
  
-   [Mover membros dentro de uma hierarquia &#40;Master Data Services&#41;](move-members-within-a-hierarchy-master-data-services.md)  
  
## <a name="see-also"></a>Consulte também  
 [Criar uma hierarquia explícita &#40;Master Data Services&#41;](../../2014/master-data-services/create-an-explicit-hierarchy-master-data-services.md)   
 [Criar um membro folha &#40;Master Data Services&#41;](../../2014/master-data-services/create-a-leaf-member-master-data-services.md)   
 [Carregar ou atualizar membros no Master Data Services por meio do processo de preparo](/sql/2014/master-data-services/add-update-and-delete-data-master-data-services)   
 [Membros &#40;Master Data Services&#41;](../../2014/master-data-services/members-master-data-services.md)   
 [Hierarquias explícitas &#40;Master Data Services&#41;](../../2014/master-data-services/explicit-hierarchies-master-data-services.md)  
  
  
