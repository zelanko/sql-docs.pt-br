---
title: Atributos (guia estrutura da dimensão, designer de dimensão) (Analysis Services-dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql.asvs.dimensiondesigner.dbv.attributespane.f1
ms.assetid: 627eaa08-7638-4edd-bdfa-0d8175a7cde5
author: minewiskan
ms.author: owend
ms.openlocfilehash: 6c5e1d6b92dce1a1be42ae1bc30ae3a3d5e48d59
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84527842"
---
# <a name="attributes-dimension-structure-tab-dimension-designer-analysis-services---multidimensional-data"></a>Atributos (guia Estrutura da Dimensão, Designer de Dimensão) (Analysis Services - Dados multidimensionais)
  Use este painel para gerenciar os atributos associados com a dimensão selecionada. Podem ser arrastados atributos deste painel para o painel **Hierarquias** para criar hierarquias e níveis. Para obter mais informações, consulte [Hierarchies &#40;Dimension Structure Tab, Dimension Designer&#41; &#40;Analysis Services - Multidimensional Data&#41;](hierarchies-dimension-designer-analysis-services-multidimensional-data.md).  
  
 Para criar um atributo, arraste uma coluna do painel **Exibição da Fonte de Dados** para o painel **Atributos** no modo de lista, de árvore ou de exibição. Para remover um atributo, selecione **Excluir** no menu de atalhos.  
  
 **Para exibir o painel Atributos**  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e então abra a dimensão desejada.  
  
2.  Se não selecionado, clique na guia **Estrutura da Dimensão** .  
  
## <a name="options"></a>Opções  
 **Atributos**  
 Exibe os atributos disponíveis para a dimensão selecionada. Esta opção pode ser exibida nos seguintes modos:  
  
-   Modo de lista  
  
     Use este modo para criar e modificar hierarquias. Para exibir os atributos em modo de lista, selecione **Mostrar Atributos em** no menu de atalhos e então clique em **Listas**.  
  
-   Modo Árvore  
  
     Use este modo para criar e modificar hierarquias. Para exibir os atributos em modo de árvore, selecione **Mostrar Atributos em** no menu de atalhos e então clique em **Árvore**.  
  
-   Modo de grade  
  
     Use este modo para criar dimensões manualmente ou para modificar propriedades de atributo. Para exibir os atributos em modo de grade, selecione **Mostrar Atributos em** no menu de atalhos e então clique em **Grade**.  
  
## <a name="grid-mode-options"></a>Opções do Modo de Grade  
 Ao exibir atributos em modo de grade, você tem acesso às colunas listadas na seguinte tabela.  
  
 **Nome**  
 Exibe o nome do atributo.  
  
 **Usage**  
 Define o uso do atributo selecionado. Clique na seta para baixo para selecionar entre as seguintes possibilidades:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|Regular|Identifica um atributo regular.|  
|Chave|Identifica o atributo de chave para a dimensão. Isto corresponde aos membros folha da dimensão. Pode haver somente um atributo de chave por dimensão. Para modificar, clique no botão de reticências (**...**) próximo à propriedade **KeyColumns** no painel **Propriedades** .|  
|Pai|Denota o atributo pai para uma relação pai-filho. O atributo filho nesta relação deve sempre ser o atributo de chave.|  
|AccountType|Denota um atributo de tipo de conta. Isto é usado pelo servidor ou mecanismo quando a função de agregação para uma medida é definida como "por conta".|  
  
 **Tipo**  
 Define o tipo do atributo. Clique na seta para baixo para selecionar entre as seguintes possibilidades.  
  
 **Coluna de chave**  
 Exibe o tipo de dados das colunas subjacentes. Ao criar um novo atributo, clique na seta para baixo para selecionar entre as possibilidades disponíveis.  
  
 **Coluna de nome**  
 Exibe o local da coluna subjacente. Ao criar um novo atributo, clique na seta para baixo para selecionar entre **Igual à chave** e **Separar coluna**. Se **Separar coluna** for escolhido, a propriedade **NameColumn** no painel **Propriedades** definirá a coluna que armazena o nome a usar para o atributo.  
  
## <a name="see-also"></a>Consulte Também  
 [Estrutura de dimensão &#40;designer de dimensão&#41; &#40;Analysis Services de dados multidimensionais&#41;](dimension-structure-dimension-designer-analysis-services-multidimensional-data.md)   
 [Hierarquias &#40;guia estrutura da dimensão, designer de dimensão&#41; &#40;Analysis Services de dados multidimensionais&#41;](hierarchies-dimension-designer-analysis-services-multidimensional-data.md)   
 [Barra de ferramentas &#40;guia estrutura da dimensão, designer de dimensão&#41; &#40;Analysis Services de dados multidimensionais&#41;](toolbar-dimension-structure-designer-analysis-services-multidimensional-data.md)  
  
  
