---
title: Mover itens de página (Gerenciador de relatórios) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: fc83b8d2-bc79-4b56-8970-34a1cbbcc176
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2f64a9e9efe180c2db776c38553403e5f7cdfac9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66108223"
---
# <a name="move-items-page-report-manager"></a>Página Mover Itens (Gerenciador de Relatórios)
  Use a página Mover Itens para mover um relatório, pasta ou outro item para um novo local no servidor de relatório. Você pode digitar o caminho do novo local ou usar uma exibição de árvore para procurar um novo local no namespace do servidor de relatório. Você só pode mover itens que tem permissão para mover e que estejam armazenados no servidor de relatório atual.  
  
 Quando você move um item referenciado por outro item (por exemplo, uma fonte de dados compartilhada ou um modelo referenciado por muitos relatórios), as informações de caminho desse item são atualizadas automaticamente. Mover uma fonte de dados compartilhada não interrompe a conexão da fonte de dados com os relatórios e modelos que ela usa. Se você mover uma fonte de dados compartilhada ou modelo para uma pasta à qual os usuários não têm permissão, eles ainda assim poderão executar qualquer relatório que referencia a fonte de dados ou o modelo, mas o item não estará visível na hierarquia de pasta.  
  
 Para **Local**, especifique o caminho completo até a pasta, começando com o nome da pasta raiz. É possível digitar o nome do caminho ou usar a exibição de árvore para navegar até a pasta desejada.  
  
> [!NOTE]  
>  Nem todos os itens podem ser movidos. Você não pode mover pastas reservadas como Base, Meu Relatórios ou Pastas de Usuários. Você não pode mover histórico de relatório ou instantâneos para locais diferentes. O histórico e os instantâneos sempre estão localizados no relatório e são acessados por meio do relatório no qual se baseiam.  
  
## <a name="navigation"></a>Navegação  
 Use os procedimentos a seguir para navegar para este local na interface do usuário.  
  
###### <a name="to-open-the-move-items-page-from-the-contents-page-in-details-view"></a>Para abrir a página Mover Itens na página Conteúdo em Exibição de Detalhes  
  
1.  Abra o Gerenciador de Relatórios e navegue até a pasta que contém um item que você deseja mover. Você também pode mover itens da Página inicial do Gerenciador de Relatórios.  
  
2.  Na barra de ferramentas, clique em **Exibição de Detalhes**.  
  
    > [!NOTE]  
    >  Caso você veja apenas **Exibição Lado a Lado**, já estará em **Exibição de Detalhes**.  
  
3.  Marque a caixa ao lado de um item e clique em **Mover** na barra de ferramentas. Você poderá selecionar mais de uma caixa se desejar mover vários itens para o mesmo local novo.  
  
###### <a name="to-open-the-move-items-page-from-the-contents-page-in-tiles-view"></a>Para abrir a página Mover Itens na página Conteúdo em Exibição Lado a Lado  
  
1.  Abra o Gerenciador de Relatórios e navegue até a pasta que contém um item que você deseja mover. Você também pode mover itens da Página inicial do Gerenciador de Relatórios.  
  
2.  Na barra de ferramentas, clique em **Exibição Lado a Lado**.  
  
    > [!NOTE]  
    >  Caso você veja apenas **Exibição de Detalhes**, já estará em **Exibição Lado a lado**.  
  
3.  Focalize um item e clique na seta do menu suspenso.  
  
4.  No menu suspenso, clique em **Mover**.  
  
###### <a name="to-open-the-move-items-page-from-the-general-properties-page-of-an-item"></a>Para abrir a página Mover Itens na página Propriedades Gerais de um item  
  
1.  Abra o Gerenciador de Relatórios e navegue até a pasta que contém um item que você deseja mover. Você também pode mover itens da Página inicial do Gerenciador de Relatórios.  
  
2.  Focalize um item e clique na seta do menu suspenso.  
  
3.  No menu suspenso, clique em **Gerenciar**. Esse procedimento abre a página Propriedades Gerais de um item.  
  
4.  Na barra de ferramentas de item, clique **Mover**.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md)   
 [Página Propriedades gerais, pastas &#40;Gerenciador de relatórios&#41;](../../2014/reporting-services/general-properties-page-folders-report-manager.md)   
 [Página Propriedades Gerais, Relatórios &#40;Gerenciador de Relatórios&#41;](../../2014/reporting-services/general-properties-page-reports-report-manager.md)   
 [Página Propriedades gerais, recursos do &#40;Gerenciador de relatórios&#41;](../../2014/reporting-services/general-properties-page-resources-report-manager.md)   
 [Página Propriedades gerais, fontes de dados &#40;Gerenciador de relatórios&#41;](../../2014/reporting-services/general-properties-page-shared-data-sources-report-manager.md)   
 [Ajuda F1 do Gerenciador de Relatórios](../../2014/reporting-services/report-manager-f1-help.md)  
  
  
