---
title: Tornar um grupo de atributos visível para os usuários (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: b2f6cc27-dbc9-4f3f-961e-e81e76375248
caps.latest.revision: 3
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 70dcc1e8f35f288b4693bd87308d7f2abcff0136
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36115239"
---
# <a name="make-an-attribute-group-visible-to-users-master-data-services"></a>Tornar um grupo de atributos visível para os usuários (Master Data Services)
  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], torne um grupo de atributos visível para usuários ou grupos quando você desejar que os usuários tenham guias acima da grade na área funcional do **Explorer** .  
  
 Quando você criar um grupo de atributos, ele será ocultado automaticamente de todos os usuários, exceto daquele que o criou.  
  
## <a name="prerequisites"></a>Prerequisites  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional **Administração do Sistema** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, veja [Administrators &#40;Master Data Services&#41;](administrators-master-data-services.md).  
  
-   Pelo menos um grupo de atributos deve existir. Para obter mais informações, veja [Create an Attribute Group &#40;Master Data Services&#41;](../../2014/master-data-services/create-an-attribute-group-master-data-services.md).  
  
### <a name="to-make-an-attribute-group-visible-to-users"></a>Para tornar um grupo de atributos visível para usuários  
  
1.  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], clique em **Administração do Sistema**.  
  
2.  Sobre o **exibição do modelo de** página, na barra de menus, aponte para **gerenciar** e clique em **grupos de atributos**.  
  
3.  Na lista **Modelo** , selecione um modelo.  
  
4.  Na lista **Entidade** , selecione uma entidade.  
  
5.  Clique no sinal de adição para expandir **grupos de folha**, **grupos consolidados**, ou **grupos de coleção**, dependendo do tipo de grupo que você deseja tornar visível.  
  
6.  Clique no sinal de adição para expandir o grupo que você deseja tornar visível.  
  
7.  Clique em **usuários** ou **grupos**, dependendo se você estiver fazendo o grupo visível para um usuário ou grupo.  
  
8.  Clique em **Editar item selecionado**.  
  
9. Clique em usuários ou grupos a **disponível** caixa e clique no **adicionar** seta. Para adicionar tudo, clique na seta **Adicionar Tudo** .  
  
10. Clique em **Salvar**.  
  
## <a name="see-also"></a>Consulte também  
 [Grupos de atributos &#40;Master Data Services&#41;](../../2014/master-data-services/attribute-groups-master-data-services.md)   
 [Criar um grupo de atributos &#40;Master Data Services&#41;](../../2014/master-data-services/create-an-attribute-group-master-data-services.md)  
  
  