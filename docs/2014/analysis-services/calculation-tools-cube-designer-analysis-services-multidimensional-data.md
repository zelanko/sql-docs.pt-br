---
title: Ferramentas de cálculo (guia cálculos, Designer de cubo) (Analysis Services - dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.calculationsview.calculationtoolspane.f1
ms.assetid: b1aa8a1a-6532-45d2-8f53-d3e211d7197a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 61aed2ac785c628d7a67df39af13aaf0a7c74914
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48104896"
---
# <a name="calculation-tools-calculations-tab-cube-designer-analysis-services---multidimensional-data"></a>Ferramentas de Cálculo (guia Cálculos, Designer de Cubo) (Analysis Services - Dados Multidimensionais)
  Use o painel **Ferramentas de Cálculo** da guia **Cálculos** no Designer de Cubo para explorar metadados, funções e modelos disponíveis para uso em cálculos.  
  
## <a name="options"></a>Opções  
 **Metadados**  
 Exibe os metadados do cubo selecionado.  
  
 Arraste um elemento selecionado para o painel Editor de Scripts, Editor de Formulário de Membro Calculado ou Editor de Formulário de Conjunto Nomeado para incluir a sintaxe MDX daquele elemento no local selecionado no painel.  
  
 **Funções**  
 Exibe as funções disponíveis para expressões e condições.  
  
 Arraste um elemento selecionado para o painel **Editor de Scripts**, **Editor de Formulário de Membro Calculado**ou **Editor de Formulário de Conjunto Nomeado** para incluir a sintaxe MDX daquele elemento no local selecionado no painel.  
  
> [!NOTE]  
>  No modo de projeto, a caixa de diálogo **Ferramentas de Cálculo** lê as informações desta opção em um arquivo XML denominado MDXFunctions.xml fornecido com o [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Em modo online, informações para esta opção são recuperadas do conjunto de linhas de esquema de MDSCHEMA_FUNCTIONS da instância.  
  
 **Modelos**  
 Exibe os modelos predefinidos disponíveis para membros calculados, conjuntos nomeados e comandos de script.  
  
 Arraste um elemento selecionado para o painel **Editor de Scripts**, **Editor de Formulário de Membro Calculado**ou **Editor de Formulário de Conjunto Nomeado** para incluir a sintaxe MDX daquele elemento no local selecionado no painel.  
  
## <a name="context-menu"></a>Menu de contexto  
 As seguintes opções estão disponíveis no menu de contexto exibido ao clicar com o botão direito do mouse em um elemento exibido no painel **Ferramentas de Cálculo** :  
  
 **Copiar**  
 Selecione para copiar o elemento selecionado em **Metadados** ou **Funções** na Área de Transferência.  
  
> [!NOTE]  
>  Esta opção não será exibida se a opção **Modelos** estiver selecionada.  
  
> [!NOTE]  
>  Esta opção será desabilitada se o membro selecionado não puder ser copiado, como a pasta **Conjuntos** de uma dimensão exibida em **Metadados** ou a pasta de grupo de funções de uma função exibida em **Funções**.  
  
 **Filtrar membros**  
 Clique para exibir a caixa de diálogo **Filtrar Membros** e filtrar os membros exibidos para o elemento selecionado em **Metadados**. Para obter mais informações sobre a caixa de diálogo **Filtrar Membros**, consulte [Caixa de diálogo Filtrar Membros &#40;Analysis Services – Dados Multidimensionais&#41;](filter-members-dialog-box-analysis-services-multidimensional-data.md).  
  
> [!NOTE]  
>  Esta opção será exibida apenas se a opção **Metadados** estiver selecionada.  
  
> [!NOTE]  
>  Esta opção estará habilitada apenas se um nível de um atributo estiver selecionado em **Metadados**.  
  
 **Adicionar modelo**  
 Selecione para adicionar um novo membro calculado, conjunto nomeado ou comando de script baseado no modelo selecionado para o script do cubo e exibir o **Editor de Scripts**, **Editor de Formulário de Membro Calculado**ou **Editor de Formulário de Conjunto Nomeado** conforme apropriado para o comando (na exibição do formulário) ou para rolar o conteúdo do painel **Editor de Scripts** para o local do comando no script do cubo (na exibição de script).  
  
> [!NOTE]  
>  Esta opção será exibida apenas se a opção **Metadados** estiver selecionada.  
  
## <a name="see-also"></a>Consulte também  
 [Designer de cubo &#40;Analysis Services - dados multidimensionais&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [Barra de ferramentas &#40;guia cálculos, Designer de cubo&#41; &#40;Analysis Services - dados multidimensionais&#41;](toolbar-calculations-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [Organizador de script &#40;guia cálculos, Designer de cubo&#41; &#40;Analysis Services - dados multidimensionais&#41;](script-organizer-cube-designer-analysis-services-multidimensional-data.md)   
 [Editor de formulário de membro calculado &#40;guia cálculos, Designer de cubo&#41; &#40;Analysis Services - dados multidimensionais&#41;](calculated-member-form-editor-cube-designer-analysis-services-multidimensional-data.md)   
 [Editor de formulário de conjunto nomeado &#40;guia cálculos, Designer de cubo&#41; &#40;Analysis Services - dados multidimensionais&#41;](named-set-form-editor-cube-designer-analysis-services-multidimensional-data.md)   
 [Editor de scripts &#40;guia cálculos, Designer de cubo&#41; &#40;Analysis Services - dados multidimensionais&#41;](script-editor-calculations-cube-designer-analysis-services-multidimensional-data.md)   
 [Cálculos de &#40;Designer de cubo&#41; &#40;Analysis Services - dados multidimensionais&#41;](calculations-cube-designer-analysis-services-multidimensional-data.md)  
  
  
