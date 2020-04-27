---
title: Mover ou excluir um item (Gerenciador de Relatórios) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- moving items
- items [Reporting Services], moving
ms.assetid: 980a66c7-a18b-4af7-8954-45726fa517d6
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: aafd2ff32e8c554186d18a6329649081e8babe6b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66103731"
---
# <a name="move-or-delete-an-item-report-manager"></a>Mover ou excluir um item (Gerenciador de Relatórios)
  Relatórios e itens de relatório que você publica em um servidor de relatório são armazenados em pastas. Você pode mover itens para uma pasta diferente e as referências a esses itens são mantidas automaticamente pelo servidor de relatório. Antes de excluir um item, verifique se outros itens dependem dele.  
  
## <a name="move-an-item"></a>Mover um item  
 Você pode mover itens do servidor de relatório para locais de pasta diferentes na hierarquia de pastas do servidor de relatório. Quando você move um item, todas as propriedades (inclusive configurações de segurança) são movidas com o item para o novo local. Ao mover uma pasta, todos os itens na pasta são movidos juntos.  
  
 No Gerenciador de Relatórios, os itens que podem ser movidos estão indicados na hierarquia de pasta. A tabela a seguir mostra o ícone para cada item móvel.  
  
|ícone|Item móvel|  
|----------|-------------------|  
|![Report icon](../media/hlp-16doc.gif "Ícone do relatório")|Relatório|  
|![Ícone do relatório vinculado](../media/hlp-16linked.gif "Ícone do relatório vinculado")|Relatório vinculado|  
|![Ícone de pasta](../media/hlp-16folder.gif "Ícone de pasta")|Pasta|  
|![ícone de recurso genérico](../media/hlp-16file.gif "ícone de recurso genérico")|Recurso genérico|  
|![Shared data source icon](../media/hlp-16datasource.png "Ícone da fonte de dados compartilhada")|Fonte de dados compartilhada|  
||Conjunto de dados compartilhado|  
  
 Nem todos os itens com os quais você trabalha podem ser movidos. Não é possível mover itens associados a um relatório, como assinaturas ou histórico de relatório. Esses itens são movidos com os seus relatórios associados. De maneira semelhante, não é possível mover itens, como agendas compartilhadas, que existem fora da hierarquia de pasta. Não é possível mover itens sem a devida permissão. A permissão para mover um item é concedida quando as seguintes tarefas são selecionadas na atribuição de função para o item em questão: "Gerenciar relatórios," "Gerenciar modelos", "Gerenciar pastas" e "Gerenciar fontes de dados".  
  
#### <a name="to-move-an-item-from-within-the-contents-page"></a>Para mover um item de dentro da página Conteúdo  
  
1.  Inicie o [Report Manager &#40;o modo nativo do SSRS&#41;].. /report-manager-ssrs-native-mode.md).  
  
2.  No Gerenciador de Relatórios, navegue até a página **Conteúdo** e localize o item que você deseja mover.  
  
3.  Focalize o item e clique na seta do menu suspenso.  
  
4.  No menu suspenso, clique em **Mover**.  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
6.  Para **Localização**, especifique a pasta para a qual você deseja mover o item. É possível digitar o nome de pasta totalmente qualificado ou usar o controle de árvore para navegar até a pasta.  
  
7.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
 Como alternativa, navegue até o objeto que você deseja mover, clique em **Propriedades**e clique em **Mover** na parte superior da página.  
  
## <a name="delete-an-item"></a>Excluir um item  
 Antes de excluir um item, determine se ele é usado por outros itens. Por exemplo, se você excluir uma fonte de dados compartilhada, relatórios e modelos que usam essa fonte de dados não serão mais executados. Se um relatório for excluído, as assinaturas e o histórico de relatórios associados também são excluídos. Para localizar itens dependentes de um item, consulte [página de itens dependentes &#40;Report Manager&#41;].. /dependent-items-page-report-manager.md).  
  
#### <a name="to-delete-a-report-or-item"></a>Para excluir um relatório ou item  
  
1.  Inicie o [Report Manager &#40;o modo nativo do SSRS&#41;].. /report-manager-ssrs-native-mode.md).  
  
2.  No Gerenciador de Relatórios, navegue até a página **Conteúdo** e localize o item que você deseja excluir.  
  
3.  Focalize o item e clique na seta do menu suspenso.  
  
4.  No menu suspenso, clique em **Excluir**.  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Página de conteúdo &#40;Report Manager&#41;].. /contents-page-report-manager.md)   
 [Localizando, exibindo e gerenciando relatórios &#40;Construtor de Relatórios e SSRS&#41;](../report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)  
  
  
