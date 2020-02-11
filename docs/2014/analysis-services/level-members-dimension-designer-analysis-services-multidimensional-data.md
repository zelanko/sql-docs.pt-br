---
title: Nível e Membros (guia navegador, designer de dimensão) (Analysis Services-dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensiondesigner.browsertab.levelsandmembers.f1
ms.assetid: 3f61e384-5b4e-4480-a7ed-b408de2fdea7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ad602710cab83e2be25a03a4da6cce0c3407493e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66078107"
---
# <a name="level-and-members-browser-tab-dimension-designer-analysis-services---multidimensional-data"></a>Nível e Membros (guia Navegador, Designer de Dimensão) (Analysis Services - Dados Multidimensionais)
  Use este painel para procurar os membros da hierarquia e linguagem atualmente selecionadas. Para selecionar uma hierarquia ou linguagem para navegar, use as opções **Hierarquia** e **Linguagem** no painel **Barra de Ferramentas** . Para obter mais informações sobre o painel Barra de Ferramentas, consulte [Toolbar &#40;Browser Tab, Dimension Designer&#41; &#40;Analysis Services - Multidimensional Data&#41;](toolbar-browser-tab-dimension-designer-analysis-services-multidimensional-data.md).  
  
## <a name="writeback-mode"></a>Modo Write-back  
 A funcionalidade deste painel alterará se o modo write-back estiver habilitado. A dimensão selecionada deverá ser habilitada para gravação (isto é, a propriedade `WriteEnabled` da dimensão deverá ser definida como verdadeira) e a dimensão deverá ser implantada em uma instância de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] para habilitar o modo write-back.  
  
 Para habilitar o modo write-back, você poderá selecionar **Write-back** no painel **Barra de Ferramentas** ou clicar com o botão direito do mouse no painel **Nível e Membros** e selecionar **Write-back** no menu de contexto.  
  
 Se o modo write-back estiver habilitado, você poderá executar as seguintes ações adicionais no painel **Nível e Membros** :  
  
|Fazer|Executar|  
|-----------|-------------|  
|Criar membros irmão e filho dentro da hierarquia selecionada.|Clique com o botão direito do mouse no membro selecionado e selecione **Criar irmão**para criar um membro irmão ou **Criar Filho**para criar um membro irmão, no menu de contexto.|  
|Mova um membro selecionado para cima ou para baixo na hierarquia.|Arraste o membro selecionado até o membro pai ou filho apropriado ou clique em **Aumentar Recuo** ou **Diminuir Recuo** no painel **Barra de Ferramentas** para mover o membro selecionado para cima ou para baixo nos níveis da hierarquia.|  
|Renomeie um membro selecionado.|Clique com o botão direito do mouse no membro selecionado e selecione **Renomear**ou clique em um membro já selecionado.|  
|Edite valores de propriedade dos membros|Clique duas vezes no valor na propriedade do membro selecionado para que o membro selecionado edite|  
  
## <a name="options"></a>Opções  
 **Nível atual**  
 Exibe o nível ao qual pertence o membro atualmente selecionado em **Árvore** .  
  
 **Três**  
 Exibe os membros da hierarquia e linguagem atualmente selecionadas.  
  
 Se as propriedades dos membros forem selecionadas da opção **Propriedades do Membro** do painel Barra de Ferramentas, cada propriedade de membro será exibida como uma coluna.  
  
 Se o modo write-back estiver habilitado, uma coluna para cada coluna de chave associada com o atributo chave na dimensão será exibida.  
  
## <a name="context-menu"></a>Menu de contexto  
 As seguintes opções estarão disponíveis no menu de contexto exibido ao clicar com o botão direito do mouse em qualquer parte do painel **Nível e Membros** do membro selecionado:  
  
 **Criar irmão**  
 Cria um membro novo no mesmo nível do membro selecionado.  
  
> [!NOTE]  
>  Esta opção só será habilitada se um membro em um nível diferente do nível (Tudo) estiver selecionado.  
  
> [!NOTE]  
>  Esta opção será exibida somente se o modo write-back for habilitado.  
  
 **Criar Filho**  
 Cria um membro novo no nível inferior próximo do membro selecionado, como um filho do membro selecionado.  
  
> [!NOTE]  
>  Esta opção só será habilitada se um membro em um nível diferente do nível inferior estiver selecionado.  
  
> [!NOTE]  
>  Esta opção será exibida somente se o modo write-back for habilitado.  
  
 **Recortar**  
 Copia os membros selecionados à área de transferência e os remove da hierarquia.  
  
> [!NOTE]  
>  Esta opção só será habilitada se um membro diferente do Todos estiver selecionado.  
  
> [!NOTE]  
>  Esta opção será exibida somente se o modo write-back for habilitado.  
  
 **Colar**  
 Cola membros anteriormente removidos usando **Recortar** imediatamente após o membro selecionado.  
  
> [!NOTE]  
>  Esta opção será exibida somente se o modo write-back for habilitado.  
  
 **Delete (excluir)**  
 Remove os membros selecionados da hierarquia.  
  
> [!NOTE]  
>  Esta opção só será habilitada se um membro diferente do Todos estiver selecionado.  
  
> [!NOTE]  
>  Esta opção será exibida somente se o modo write-back for habilitado.  
  
 **Nome**  
 Selecione para editar o nome do membro selecionado.  
  
> [!NOTE]  
>  Esta opção só será habilitada se um membro diferente do Todos estiver selecionado.  
  
> [!NOTE]  
>  Esta opção será exibida somente se o modo write-back for habilitado.  
  
 **Filtrar Membros**  
 Exibe a caixa de diálogo **Filtrar Membros** para filtrar membros exibidos em **Nível e Membros** da hierarquia selecionada. Para obter mais informações sobre a caixa de diálogo **Filtrar Membros**, consulte [Caixa de diálogo Filtrar Membros &#40;Analysis Services – Dados Multidimensionais&#41;](filter-members-dialog-box-analysis-services-multidimensional-data.md).  
  
 **Expandir Tudo**  
 Expande todos os membros em **Árvore**.  
  
> [!NOTE]  
>  Esta opção só será habilitada se um membro em um nível diferente do nível inferior estiver selecionado.  
  
 **Recolher Tudo**  
 Recolhe todos os membros em **Árvore**.  
  
 **Expandir Membros**  
 Expande o membro selecionado em **Árvore**.  
  
 **Recolher Membro**  
 Recolhe o membro selecionado em **Árvore**.  
  
 **-**  
 Selecione para habilitar o modo write-back.  
  
## <a name="see-also"></a>Consulte Também  
 [Barra de ferramentas &#40;guia navegador, designer de dimensão&#41; &#40;Analysis Services de dados multidimensionais&#41;](toolbar-browser-tab-dimension-designer-analysis-services-multidimensional-data.md)   
 [Navegador &#40;designer de dimensão&#41; &#40;Analysis Services de dados multidimensionais&#41;](browser-dimension-designer-analysis-services-multidimensional-data.md)  
  
  
