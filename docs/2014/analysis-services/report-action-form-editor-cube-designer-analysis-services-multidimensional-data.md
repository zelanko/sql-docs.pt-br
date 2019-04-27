---
title: Editor de formulário de ação de relatório (guia Ações, Designer de cubo) (Analysis Services - dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.actionexpression.reportaction.f1
ms.assetid: cebfdd07-e376-46d6-86ef-b6f816a2f360
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bb8659f916fa32c7b5c944bb525e64cf0551b0d1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62748378"
---
# <a name="report-action-form-editor-actions-tab-cube-designer-analysis-services---multidimensional-data"></a>Editor de Formulário de Ação de Relatório (guia Ações, Designer de Cubo) (Analysis Services - Dados Multidimensionais)
  Use o painel **Editor de Formulário de Ação de Relatório** na guia **Ações** do Designer de Cubo para modificar a ação de relatório selecionada no painel **Organizador de Ações**.  
  
## <a name="options"></a>Opções  
 **Nome**  
 Digite o nome da ação.  
  
 **Destino da Ação**  
 Expanda para exibir as opções **Tipo de destino** e **Objeto de destino** .  
  
 **Tipo de destino**  
 Selecione o tipo de objeto ao qual a ação deve ser associada. O servidor retorna ao cliente apenas as ações que se aplicam ao objeto do tipo especificado. A ação estará disponível para o cliente se a **Condição** for atendida e se os objetos especificados na tabela a seguir estiverem selecionados.  
  
|Valor|Objeto Selecionado|  
|-----------|---------------------|  
|Membros de atributo|Um membro é selecionado de um nível baseado no atributo em **Objeto de destino**.<br /><br /> Observação: Outras hierarquias de usuário que usam o atributo selecionado herdam a ação de relatório.|  
|Células|O conjunto nomeado em **Objeto de destino** é selecionado. Selecione **Todas as células** para selecionar todas as células no cubo.|  
|Cube|O cubo em **Objeto de destino** é selecionado. Selecione CURRENTCUBE para usar o cubo atual.<br /><br /> Observação: Uso de CURRENTCUBE fornece portabilidade adicional em casos em que o cubo pode ser renomeado ou a ação copiada para outros cubos. É recomendável usar CURRENTCUBE para representar o cubo atual.|  
|Membros de dimensão|Um membro da dimensão em **Objeto de destino** é selecionado.|  
|Hierarquia|A hierarquia do **Objeto de destino** é selecionada.|  
|Membros de hierarquia|Um membro dentro da hierarquia do **Objeto de destino** é selecionado.|  
|Nível|O nível em **Objeto de destino** é selecionado.|  
|Membros de nível|Um membro dentro do nível em **Objeto de destino** é selecionado.|  
  
 **Objeto de destino**  
 Selecione o objeto ao qual a ação deve ser associada. A instância do [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] retorna ao cliente apenas as ações que se aplicam ao objeto selecionado. A lista de objetos disponíveis é restrita pela escolha de **Tipo de destino**.  
  
 **Condição (Opcional)**  
 Digite a expressão MDX que descreve uma condição opcional usada em conjunto com **Objeto de destino**que restringe ainda mais quando a ação está disponível. A expressão deve retornar um valor booliano que, se verdadeiro, indicará que a ação está disponível.  
  
 Arraste elementos selecionados do painel **Ferramentas de Cálculo** para esta opção para incluir a sintaxe MDX para o elemento selecionado.  
  
 **Servidor de relatório**  
 Expanda para exibir as opções **Nome do servidor**, **Caminho do servidor**e **Formato do relatório** .  
  
 **Nome do servidor**  
 Digite o nome da instância do [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] na qual a ação executa o relatório.  
  
 **Caminho do servidor**  
 Digite o caminho para o relatório na instância do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . Por exemplo, digite **Vendas/VendasAnuaisPorCategoria**.  
  
 **Formato do relatório**  
 Selecione o formato no qual o relatório é retornado. A tabela a seguir descreve os formatos disponíveis.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|HTML5|O relatório é retornado em um formato compatível com o HTML 5.0.|  
|HTML3|O relatório é retornado em um formato compatível com o HTML 3.2.|  
|Excel|O relatório é retornado como um arquivo de pasta de trabalho [!INCLUDE[msCoName](../includes/msconame-md.md)] Office Excel (.xls).|  
|PDF|O relatório é retornado como um arquivo Adobe Portable Document Format (.pdf).|  
  
 **Parâmetros (Opcional)**  
 Expanda para exibir uma grade na qual os parâmetros do relatório podem ser fornecidos para o relatório especificado em **Relatório**. A grade contém as seguintes colunas:  
  
|coluna|Descrição|  
|------------|-----------------|  
|**Nome do parâmetro**|Digite o nome do parâmetro de relatório a ser passado para o relatório.|  
|**Valor do Parâmetro**|Digite o valor do parâmetro de relatório a ser passado para o relatório.<br /><br /> Clique no botão de reticências (**...**) para exibir a caixa de diálogo **Construtor MDX** e crie uma expressão MDX que forneça o valor do parâmetro de relatório. Para obter mais informações sobre a caixa de diálogo **Construtor MDX**, consulte [Construtor MDX &#40;Analysis Services – Dados Multidimensionais&#41;](mdx-builder-analysis-services-multidimensional-data.md).<br /><br /> Se o parâmetro estiver definido como uma expressão MDX, a expressão será avaliada quando a ação for executada. Caso contrário ela será passada para o relatório sem modificação.|  
  
 **Propriedades Adicionais**  
 Expanda para exibir as opções **Invocação**, **Aplicativo**, **Descrição**, **Legenda**e **A legenda é MDX** .  
  
 **Invocação**  
 Selecione a configuração que indica quando a ação deve ser executada.  
  
> [!NOTE]  
>  Essa opção fornece apenas uma recomendação a um aplicativo cliente em relação a quando executar uma ação e não controla diretamente a invocação da ação.  
  
 A tabela a seguir descreve as configurações disponíveis.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|Lote|A ação deve ser executada como parte de uma operação em lote ou de uma tarefa do [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .|  
|Interativo|A ação é executada quando o usuário a invoca.|  
|Em Aberto|A ação é executada quando o cubo é aberto pela primeira vez.|  
  
 **Aplicativo**  
 Digite o nome do aplicativo que pode interpretar a cadeia de caracteres retornada por **Expressão da ação**.  
  
 Também é possível usar essa opção para identificar qual aplicativo cliente usa essa ação mais comumente, bem como para exibir ícones adequados ao lado da ação em um menu pop-up.  
  
> [!NOTE]  
>  Essa opção fornece apenas uma recomendação a um aplicativo cliente quanto a qual aplicativo cliente deve executar uma ação e não controla diretamente o acesso à ação. Aplicativos cliente devem ocultar todas as ações associadas a outros aplicativos cliente.  
  
 **Descrição**  
 Digite a descrição opcional da ação.  
  
 **Caption**  
 Digite a legenda a ser exibida para a ação no aplicativo cliente, se a opção **A legenda é MDX** estiver configurada como **Falso**.  
  
 Digite a expressão MDX que retornará uma cadeia de caracteres para a legenda, se a opção **A legenda é MDX** estiver configurada como **Verdadeiro**.  
  
 **A legenda é MDX**  
 Selecione **Falso** para indicar que a **Legenda** contém uma cadeia de caracteres literal que representa uma legenda a ser exibida para a ação no aplicativo cliente.  
  
 Selecione **Verdadeiro** para indicar que a **Legenda** contém uma expressão MDX que retorna uma cadeia de caracteres que representa uma legenda a ser exibida para a ação no aplicativo cliente. A expressão MDX deve ser resolvida antes da ação ser retornada ao aplicativo cliente.  
  
## <a name="see-also"></a>Consulte também  
 [Ações &#40;Designer de cubo&#41; &#40;Analysis Services - dados multidimensionais&#41;](actions-cube-designer-analysis-services-multidimensional-data.md)   
 [Barra de ferramentas &#40;guia Ações, Designer de cubo&#41; &#40;Analysis Services - dados multidimensionais&#41;](toolbar-actions-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [Organizador de ações &#40;guia Ações, Designer de cubo&#41; &#40;Analysis Services - dados multidimensionais&#41;](action-organizer-cube-designer-analysis-services-multidimensional-data.md)   
 [Ferramentas de cálculo de &#40;guia Ações, Designer de cubo&#41; &#40;Analysis Services - dados multidimensionais&#41;](calculation-tools-actions-cube-designer-analysis-services-multidimensional-data.md)   
 [Editor de formulário de ação &#40;guia Ações, Designer de cubo&#41; &#40;Analysis Services - dados multidimensionais&#41;](action-form-editor-cube-designer-analysis-services-multidimensional-data.md)   
 [Editor de formulário de ação de detalhamento &#40;guia Ações, Designer de cubo&#41; &#40;Analysis Services - dados multidimensionais&#41;](drillthrough-action-form-editor-cube-designer-analysis-services-multidimensional-data.md)  
  
  
