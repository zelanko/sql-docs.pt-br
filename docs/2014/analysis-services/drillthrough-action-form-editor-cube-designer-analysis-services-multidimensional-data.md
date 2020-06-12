---
title: Editor de formulário de ação de detalhamento (guia ações, designer de cubo) (Analysis Services-dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.actionexpression.drillthroughaction.f1
ms.assetid: 225fd818-b5ea-494f-b67b-66e09798274a
author: minewiskan
ms.author: owend
ms.openlocfilehash: 546448bd05f3af45b7093acb2dbb9d1e1a8f1bd5
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84528492"
---
# <a name="drillthrough-action-form-editor-actions-tab-cube-designer-analysis-services---multidimensional-data"></a>Editor de Formulário de Ação de Extração de Detalhes (guia Ações, Designer de Cubo) (Analysis Services - Dados Multidimensionais)
  Use o painel **Editor de Formulário de Ação de Extração de Detalhes** na guia **Ações** no Designer de Cubo para modificar a ação de extração de detalhes selecionada no painel **Organizador de Ações** . Para obter mais informações sobre ações de detalhamento, consulte [Ações &#40;Analysis Services – Dados Multidimensionais&#41;](multidimensional-models/actions-analysis-services-multidimensional-data.md).  
  
> [!NOTE]  
>  Ações de extração de detalhes não fazem mais busca detalhada no repositório de dados subjacente. A informações acessadas por ações de extração de detalhes devem ser modeladas dentro do cubo usando membros de dimensão ou de hierarquia.  
  
## <a name="options"></a>Opções  
 **name**  
 Digite o nome da ação.  
  
 **Destino da Ação**  
 Expanda para exibir a opção **Membros de grupos de medidas** .  
  
 **Membros de grupos de medidas**  
 Selecione o grupo de medidas ao qual a ação de extração de detalhes deve ser associada.  
  
 **Condição (Opcional)**  
 Digite a expressão MDX que descreve uma condição opcional usada em conjunto com **Membros de grupos de medidas**que restringe ainda mais quando a ação está disponível. A expressão deve retornar um valor booliano que, se verdadeiro, indicará que a ação está disponível.  
  
 Arraste elementos selecionados do painel **Ferramentas de Cálculo** para esta opção para incluir a sintaxe MDX para o elemento selecionado.  
  
 **Colunas de Extração de Detalhes**  
 Expanda para exibir uma grade na qual indicar os atributos retornados quando o usuário executar esta ação.  
  
> [!NOTE]  
>  É possível selecionar mais do que uma dimensão, mas nenhuma dimensão pode ser usada mais de uma vez em uma ação de extração de detalhes.  
  
 A grade contém as seguintes colunas:  
  
|Coluna|Descrição|  
|------------|-----------------|  
|**Dimensões**|Selecione a dimensão da qual o atributo retornado é derivado. Selecione MEDIDAS para extração de detalhes em medidas.|  
|**Colunas de Retorno**|Selecione o atributo ou medida da dimensão selecionada a ser retornada quando a ação for executada.|  
  
 **Propriedades Adicionais**  
 Expanda para exibir as opções **Padrão**, **Máximo de linhas**, **Invocação**, **Aplicativo**, **Descrição**, **Legenda**e **A legenda é MDX** .  
  
 **Default**  
 Selecione **True** para incluir esta como uma ação de detalhamento padrão; caso contrário, selecione **False**.  
  
 Se a `RETURN` cláusula for omitida de uma `DRILLTHROUGH` instrução MDX executada por um aplicativo cliente, a [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] instância avaliará todas as ações de detalhamento padrão e executará a primeira ação de detalhamento padrão que retorna um conjunto não vazio. Para obter mais informações sobre a `DRILLTHROUGH` instrução MDX, consulte [instrução de detalhamento &#40;MDX&#41;](/sql/mdx/mdx-data-manipulation-drillthrough).  
  
> [!NOTE]  
>  Esta opção é usada para fins de compatibilidade com versões anteriores.  
  
 **Máximo de linhas**  
 Digite o número máximo de linhas a serem retornadas pela ação de extração de detalhes. A configuração desta opção como zero ou como um valor vazio indica que a ação de extração de detalhes retorna todas as linhas recuperadas pela ação ao aplicativo cliente.  
  
 **Invocação**  
 Selecione a configuração que indica quando a ação deve ser executada.  
  
> [!NOTE]  
>  Essa opção fornece apenas uma recomendação a um aplicativo cliente em relação a quando executar uma ação e não controla diretamente a invocação da ação.  
  
 A tabela a seguir descreve as configurações disponíveis.  
  
|Valor|Description|  
|-----------|-----------------|  
|Lote|A ação deve ser executada como parte de uma operação em lote ou de uma tarefa do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .|  
|Interativo|A ação é executada quando o usuário a invoca.|  
|Em Aberto|A ação é executada quando o cubo é aberto pela primeira vez.|  
  
 **Aplicativo**  
 Digite o nome do aplicativo que pode executar a ação de extração de detalhes.  
  
 Também é possível usar essa opção para identificar qual aplicativo cliente usa essa ação mais comumente, bem como para exibir ícones adequados ao lado da ação em um menu pop-up.  
  
> [!NOTE]  
>  Essa opção fornece apenas uma recomendação a um aplicativo cliente quanto a qual aplicativo cliente deve executar uma ação e não controla diretamente o acesso à ação. Aplicativos cliente devem ocultar todas as ações associadas a outros aplicativos cliente.  
  
 **Descrição**  
 Digite a descrição opcional da ação.  
  
 **Legenda**  
 Digite a legenda a ser exibida para a ação no aplicativo cliente, se a opção **A legenda é MDX** estiver configurada como **Falso**.  
  
 Digite a expressão MDX que retornará uma cadeia de caracteres para a legenda se a opção **A legenda é MDX** estiver configurada como **True**.  
  
 **Legenda é MDX**  
 Selecione **Falso** para indicar que a **Legenda** contém uma cadeia de caracteres literal que representa uma legenda a ser exibida para a ação no aplicativo cliente.  
  
 Selecione **Verdadeiro** para indicar que a **Legenda** contém uma expressão MDX que retorna uma cadeia de caracteres que representa uma legenda a ser exibida para a ação no aplicativo cliente. A expressão MDX deve ser resolvida antes da ação ser retornada ao aplicativo cliente.  
  
## <a name="see-also"></a>Consulte Também  
 [Expressões multidimensionais &#40;referência de&#41; MDX](/sql/mdx/multidimensional-expressions-mdx-reference)   
 [Ações &#40;designer de cubo&#41; &#40;Analysis Services de dados multidimensionais&#41;](actions-cube-designer-analysis-services-multidimensional-data.md)   
 [Barra de ferramentas &#40;guia ações, designer de cubo&#41; &#40;Analysis Services de dados multidimensionais&#41;](toolbar-actions-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [Guia ações do organizador de ação &#40;, designer de cubo&#41; &#40;Analysis Services de dados multidimensionais&#41;](action-organizer-cube-designer-analysis-services-multidimensional-data.md)   
 [Ferramentas de cálculo &#40;guia ações, designer de cubo&#41; &#40;Analysis Services de dados multidimensionais&#41;](calculation-tools-actions-cube-designer-analysis-services-multidimensional-data.md)   
 [Editor de formulário de ação &#40;guia ações, designer de cubo&#41; &#40;Analysis Services de dados multidimensionais&#41;](action-form-editor-cube-designer-analysis-services-multidimensional-data.md)   
 [Editor de formulário de ação de relatório &#40;guia ações, designer de cubo&#41; &#40;Analysis Services de dados multidimensionais&#41;](report-action-form-editor-cube-designer-analysis-services-multidimensional-data.md)  
  
  
