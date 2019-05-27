---
title: Editor de formulário de ação de extração de detalhes (guia Ações, Designer de cubo) (Analysis Services - dados multidimensionais) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 33d20da736308b4436c40a50b8b01da7445663c8
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66081463"
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
  
 **Membros do grupo de medidas**  
 Selecione o grupo de medidas ao qual a ação de extração de detalhes deve ser associada.  
  
 **Condição (Opcional)**  
 Digite a expressão MDX que descreve uma condição opcional usada em conjunto com **Membros de grupos de medidas**que restringe ainda mais quando a ação está disponível. A expressão deve retornar um valor booliano que, se verdadeiro, indicará que a ação está disponível.  
  
 Arraste elementos selecionados do painel **Ferramentas de Cálculo** para esta opção para incluir a sintaxe MDX para o elemento selecionado.  
  
 **Colunas de Extração de Detalhes**  
 Expanda para exibir uma grade na qual indicar os atributos retornados quando o usuário executar esta ação.  
  
> [!NOTE]  
>  É possível selecionar mais do que uma dimensão, mas nenhuma dimensão pode ser usada mais de uma vez em uma ação de extração de detalhes.  
  
 A grade contém as seguintes colunas:  
  
|coluna|Descrição|  
|------------|-----------------|  
|**Dimensions**|Selecione a dimensão da qual o atributo retornado é derivado. Selecione MEDIDAS para extração de detalhes em medidas.|  
|**Colunas de retorno**|Selecione o atributo ou medida da dimensão selecionada a ser retornada quando a ação for executada.|  
  
 **Propriedades Adicionais**  
 Expanda para exibir as opções **Padrão**, **Máximo de linhas**, **Invocação**, **Aplicativo**, **Descrição**, **Legenda**e **A legenda é MDX** .  
  
 **Default**  
 Selecione **True** para incluir esta como uma ação de detalhamento padrão; caso contrário, selecione **False**.  
  
 Se o `RETURN` cláusula for omitida de uma MDX `DRILLTHROUGH` instrução executada por um aplicativo cliente, o [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] instância avalia todas as ações de detalhamento padrão e é executado primeiro detalhamento padrão ação que retorna um conjunto não vazio. Para obter mais informações sobre o MDX `DRILLTHROUGH` instrução, consulte [instrução DRILLTHROUGH &#40;MDX&#41;](/sql/mdx/mdx-data-manipulation-drillthrough).  
  
> [!NOTE]  
>  Esta opção é usada para fins de compatibilidade com versões anteriores.  
  
 **Máximo de linhas**  
 Digite o número máximo de linhas a serem retornadas pela ação de extração de detalhes. A configuração desta opção como zero ou como um valor vazio indica que a ação de extração de detalhes retorna todas as linhas recuperadas pela ação ao aplicativo cliente.  
  
 **Invocação**  
 Selecione a configuração que indica quando a ação deve ser executada.  
  
> [!NOTE]  
>  Essa opção fornece apenas uma recomendação a um aplicativo cliente em relação a quando executar uma ação e não controla diretamente a invocação da ação.  
  
 A tabela a seguir descreve as configurações disponíveis.  
  
|Valor|Descrição|  
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
  
 **Caption**  
 Digite a legenda a ser exibida para a ação no aplicativo cliente, se a opção **A legenda é MDX** estiver configurada como **Falso**.  
  
 Digite a expressão MDX que retornará uma cadeia de caracteres para a legenda se a opção **A legenda é MDX** estiver configurada como **True**.  
  
 **A legenda é MDX**  
 Selecione **Falso** para indicar que a **Legenda** contém uma cadeia de caracteres literal que representa uma legenda a ser exibida para a ação no aplicativo cliente.  
  
 Selecione **Verdadeiro** para indicar que a **Legenda** contém uma expressão MDX que retorna uma cadeia de caracteres que representa uma legenda a ser exibida para a ação no aplicativo cliente. A expressão MDX deve ser resolvida antes da ação ser retornada ao aplicativo cliente.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de expressões multidimensionais &#40;MDX&#41;](/sql/mdx/multidimensional-expressions-mdx-reference)   
 [Ações &#40;Designer de cubo&#41; &#40;Analysis Services - dados multidimensionais&#41;](actions-cube-designer-analysis-services-multidimensional-data.md)   
 [Barra de ferramentas &#40;guia Ações, Designer de cubo&#41; &#40;Analysis Services - dados multidimensionais&#41;](toolbar-actions-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [Organizador de ações &#40;guia Ações, Designer de cubo&#41; &#40;Analysis Services - dados multidimensionais&#41;](action-organizer-cube-designer-analysis-services-multidimensional-data.md)   
 [Ferramentas de cálculo de &#40;guia Ações, Designer de cubo&#41; &#40;Analysis Services - dados multidimensionais&#41;](calculation-tools-actions-cube-designer-analysis-services-multidimensional-data.md)   
 [Editor de formulário de ação &#40;guia Ações, Designer de cubo&#41; &#40;Analysis Services - dados multidimensionais&#41;](action-form-editor-cube-designer-analysis-services-multidimensional-data.md)   
 [Editor de formulário de ação de relatório &#40;guia Ações, Designer de cubo&#41; &#40;Analysis Services - dados multidimensionais&#41;](report-action-form-editor-cube-designer-analysis-services-multidimensional-data.md)  
  
  
