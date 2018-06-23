---
title: Editor de formulário de ação (guia Ações, Designer de cubo) (Analysis Services - dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.cubeeditor.actionexpression.action.f1
ms.assetid: c363a29b-6099-473c-9625-460cc15b3d95
caps.latest.revision: 24
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 7ce8acc1630b9944b2ac858ba27a1f515bb19adc
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36117292"
---
# <a name="action-form-editor-actions-tab-cube-designer-analysis-services---multidimensional-data"></a>Editor de Formulário de Ação (guia Ações, Designer de Cubo) (Analysis Services - Dados Multidimensionais)
  Use o painel Editor de Formulário de Ação na guia **Ações** do Designer de Cubo para criar e modificar ações padrão.  
  
## <a name="options"></a>Opções  
 **Nome**  
 Digite o nome da ação.  
  
 **Destino da Ação**  
 Expanda para exibir as opções **Tipo de destino** e **Objeto de destino** .  
  
 **Tipo de destino**  
 Selecione o tipo de objeto ao qual a ação deve ser associada. O servidor retorna ao cliente apenas as ações que se aplicam ao objeto do tipo especificado. A ação estará disponível para o cliente se a **Condição** for atendida e se os objetos especificados na tabela a seguir estiverem selecionados.  
  
|Valor|Objeto Selecionado|  
|-----------|---------------------|  
|Membros de atributo|Um membro é selecionado de um nível baseado no atributo em **Objeto de destino**.|  
|Células|O conjunto nomeado em **Objeto de destino** é selecionado. Selecione **Todas as células** para selecionar todas as células no cubo.|  
|Cube|O cubo em **Objeto de destino** é selecionado. Selecione CURRENTCUBE para usar o cubo atual.<br /><br /> Observação: o uso de CURRENTCUBE fornece portabilidade adicional em casos nos quais o cubo possa ser renomeado ou a ação copiada para outros cubos. É recomendável usar CURRENTCUBE para representar o cubo atual.|  
|Membros de dimensão|Um membro da dimensão em **Objeto de destino** é selecionado.|  
|Hierarquia|A hierarquia do **Objeto de destino** é selecionada.|  
|Membros de hierarquia|Um membro dentro da hierarquia do **Objeto de destino** é selecionado.|  
|Nível|O nível em **Objeto de destino** é selecionado.|  
|Membros de nível|Um membro dentro do nível em **Objeto de destino** é selecionado.|  
  
 **Objeto de destino**  
 Selecione o objeto ao qual a ação deve ser associada. A instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] retorna ao cliente apenas as ações que se aplicam ao objeto selecionado. A lista de objetos disponíveis é restrita pela escolha de **Tipo de destino**.  
  
 **Condição (Opcional)**  
 Digite a expressão MDX que descreve uma condição opcional usada em conjunto com **Objeto de destino**que restringe ainda mais quando a ação está disponível. A expressão deve retornar um valor booliano que, se verdadeiro, indicará que a ação está disponível.  
  
 Arraste elementos selecionados do painel **Ferramentas de Cálculo** para esta opção para incluir a sintaxe MDX para o elemento selecionado.  
  
 **Conteúdo da Ação**  
 Expanda para exibir as opções **Tipo** e **Expressão da Ação** .  
  
 **Tipo**  
 Selecione o tipo de ação a ser tomada quando a ação for executada. Os seguintes tipos de ação estão disponíveis:  
  
|Valor|Description|  
|-----------|-----------------|  
|Dataset|Retorna uma instrução MDX representando um conjunto de dados multidimensional a ser executado e exibido pelo aplicativo cliente.|  
|Proprietário|Retorna uma cadeia de caracteres proprietária que pode ser interpretada por aplicativos cliente associados à configuração **Aplicativo** para esta ação.|  
|Conjunto de linhas|Retorna uma instrução MDX representando um conjunto de linhas tabular a ser executado e exibido pelo aplicativo cliente.|  
|de|Retorna uma cadeia de caracteres do comando a ser executado pelo aplicativo cliente.|  
|URL|Retorna a cadeia de caracteres de uma URL a ser aberta pelo aplicativo cliente, normalmente com um navegador da Internet.|  
  
 Para obter mais informações sobre tipos de ações, consulte [Ações &#40;Analysis Services – Dados Multidimensionais&#41;](multidimensional-models/actions-analysis-services-multidimensional-data.md).  
  
 **Expressão da ação**  
 Digite a expressão MDX que retorna a cadeia de caracteres retornada pela ação ao aplicativo cliente para execução.  
  
 **Propriedades Adicionais**  
 Expanda para exibir as opções **Invocação**, **Aplicativo**, **Descrição**, **Legenda**e **A legenda é MDX** .  
  
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
 Digite o nome do aplicativo que pode interpretar a cadeia de caracteres retornada por **Expressão da ação**.  
  
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
 [Ações &#40;Designer de cubo&#41; &#40;Analysis Services - dados multidimensionais&#41;](actions-cube-designer-analysis-services-multidimensional-data.md)   
 [Barra de ferramentas &#40;guia Ações, Designer de cubo&#41; &#40;Analysis Services - dados multidimensionais&#41;](toolbar-actions-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [Organizador de ações &#40;guia Ações, Designer de cubo&#41; &#40;Analysis Services - dados multidimensionais&#41;](action-organizer-cube-designer-analysis-services-multidimensional-data.md)   
 [Ferramentas de cálculo &#40;guia Ações, Designer de cubo&#41; &#40;Analysis Services - dados multidimensionais&#41;](calculation-tools-actions-cube-designer-analysis-services-multidimensional-data.md)   
 [Editor de formulário de ação de detalhamento &#40;guia Ações, Designer de cubo&#41; &#40;Analysis Services - dados multidimensionais&#41;](drillthrough-action-form-editor-cube-designer-analysis-services-multidimensional-data.md)   
 [Editor de formulário de ação de relatório &#40;guia Ações, Designer de cubo&#41; &#40;Analysis Services - dados multidimensionais&#41;](report-action-form-editor-cube-designer-analysis-services-multidimensional-data.md)  
  
  