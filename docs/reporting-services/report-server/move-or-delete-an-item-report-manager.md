---
title: "Mover ou excluir um Item (Gerenciador de relatórios) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- moving items
- items [Reporting Services], moving
ms.assetid: 980a66c7-a18b-4af7-8954-45726fa517d6
caps.latest.revision: 45
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ede41000be34b24f362518e8963cee97db3e4a66
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="move-or-delete-an-item-report-manager"></a>Mover ou excluir um item (Gerenciador de Relatórios)
  Relatórios e itens de relatório que você publica em um servidor de relatório são armazenados em pastas. Você pode mover itens para uma pasta diferente e as referências a esses itens são mantidas automaticamente pelo servidor de relatório. Antes de excluir um item, verifique se outros itens dependem dele.  
  
## <a name="move-an-item"></a>Mover um item  
 Você pode mover itens do servidor de relatório para locais de pasta diferentes na hierarquia de pastas do servidor de relatório. Quando você move um item, todas as propriedades (inclusive configurações de segurança) são movidas com o item para o novo local. Ao mover uma pasta, todos os itens na pasta são movidos juntos.  
  
 No Gerenciador de Relatórios, os itens que podem ser movidos estão indicados na hierarquia de pasta. A tabela a seguir mostra o ícone para cada item móvel.  
  
|Ícone|Item móvel|  
|----------|-------------------|  
|![Ícone de relatório](../../reporting-services/report-server/media/hlp-16doc.gif "ícone de relatório")|Relatório|  
|![Ícone de relatório vinculado](../../reporting-services/report-server/media/hlp-16linked.gif "ícone de relatório vinculado")|Relatório vinculado|  
|![Ícone de pasta](../../reporting-services/report-server/media/hlp-16folder.gif "ícone de pasta")|Pasta|  
|![ícone de recurso genérico](../../reporting-services/report-server/media/hlp-16file.gif "ícone de recurso genérico")|Recurso genérico|  
|![Ícone de fonte de dados compartilhado](../../reporting-services/report-data/media/hlp-16datasource.png "ícone de fonte de dados compartilhado")|Fonte de dados compartilhada|  
||Conjunto de dados compartilhado|  
  
 Nem todos os itens com os quais você trabalha podem ser movidos. Não é possível mover itens associados a um relatório, como assinaturas ou histórico de relatório. Esses itens são movidos com os seus relatórios associados. De maneira semelhante, não é possível mover itens, como agendas compartilhadas, que existem fora da hierarquia de pasta. Não é possível mover itens sem a devida permissão. A permissão para mover um item é concedida quando as seguintes tarefas são selecionadas na atribuição de função para o item em questão: "Gerenciar relatórios," "Gerenciar modelos", "Gerenciar pastas" e "Gerenciar fontes de dados".  
  
#### <a name="to-move-an-item-from-within-the-contents-page"></a>Para mover um item de dentro da página Conteúdo  
  
1.  Inicie o [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896).  
  
2.  No Gerenciador de Relatórios, navegue até a página **Conteúdo** e localize o item que você deseja mover.  
  
3.  Focalize o item e clique na seta do menu suspenso.  
  
4.  No menu suspenso, clique em **Mover**.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
6.  Para **Localização**, especifique a pasta para a qual você deseja mover o item. É possível digitar o nome de pasta totalmente qualificado ou usar o controle de árvore para navegar até a pasta.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 Como alternativa, navegue até o objeto que você deseja mover, clique em **Propriedades**e clique em **Mover** na parte superior da página.  
  
## <a name="delete-an-item"></a>Excluir um item  
 Antes de excluir um item, determine se ele é usado por outros itens. Por exemplo, se você excluir uma fonte de dados compartilhada, relatórios e modelos que usam essa fonte de dados não serão mais executados. Se um relatório for excluído, as assinaturas e o histórico de relatórios associados também são excluídos. Para encontrar itens dependentes para um item, consulte [Página Itens Dependentes &#40;Gerenciador de Relatórios&#41;](http://msdn.microsoft.com/library/4dcfb311-e9c3-4c5d-b2e0-018d79f37d2e).  
  
#### <a name="to-delete-a-report-or-item"></a>Para excluir um relatório ou item  
  
1.  Inicie o [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896).  
  
2.  No Gerenciador de Relatórios, navegue até a página **Conteúdo** e localize o item que você deseja excluir.  
  
3.  Focalize o item e clique na seta do menu suspenso.  
  
4.  No menu suspenso, clique em **Excluir**.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Página Conteúdo &#40;Gerenciador de Relatórios&#41;](http://msdn.microsoft.com/library/6b16869b-158a-4934-9c85-bee934b35378)   
 [Localizando, exibindo e gerenciando relatórios &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)  
  
  
