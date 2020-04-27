---
title: Mover membros dentro de uma hierarquia (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- hierarchies [Master Data Services], moving members
- explicit hierarchies, moving members
- derived hierarchies, moving members
- members [Master Data Services], moving
ms.assetid: 049c9a15-89c1-478c-8438-028fffc9e187
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 58b39d2dc660fd51d1ba21308ff056874a239731
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66054086"
---
# <a name="move-members-within-a-hierarchy-master-data-services"></a>Mover membros dentro de uma hierarquia (Master Data Services)
  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], mova os membros dentro de uma hierarquia para alterar seu local ou atribuição pai.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional do **Gerenciador** .  
  
-   Para hierarquias explícitas, você deve ter, no mínimo, a permissão **Atualizar** para a entidade.  
  
-   Para hierarquias derivadas, você deve ter um mínimo de **atualização** para o modelo e para qualquer atributo baseado em domínio usado na hierarquia.  
  
### <a name="to-move-members-within-a-hierarchy"></a>Para mover membros dentro de uma hierarquia  
  
1.  Na home page do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , na lista **Modelo** , selecione um modelo.  
  
2.  Na lista **Versão** , selecione uma versão.  
  
3.  Clique em **Gerenciador**.  
  
4.  Na barra de menus, aponte para **hierarquias** e clique em *hierarchy_name*.  
  
5.  No painel **hierarquia** , em que a hierarquia é exibida em uma estrutura de árvore, clique na caixa de seleção de cada membro que você deseja mover.  
  
6.  Na parte superior do painel **hierarquia** , clique em **recortar**.  
  
7.  No painel **hierarquia** , clique na caixa de seleção do membro para o qual você deseja mover os membros.  
  
8.  Clique em **colar**.  
  
    > [!NOTE]  
    >  Em hierarquias derivadas, você somente pode mover os membros para o mesmo nível. Além disso, não pode alterar a ordem de classificação dos membros.  
  
## <a name="see-also"></a>Consulte Também  
 [Mover membros de hierarquia explícitos usando o processo de preparo &#40;Master Data Services&#41;](add-update-and-delete-data-master-data-services.md)   
 [Hierarquias derivadas &#40;Master Data Services&#41;](../../2014/master-data-services/derived-hierarchies-master-data-services.md)   
 [Hierarquias explícitas &#40;Master Data Services&#41;](../../2014/master-data-services/explicit-hierarchies-master-data-services.md)  
  
  
