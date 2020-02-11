---
title: Consultas de detalhamento (mineração de dados) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- AllowDrillThrough property
- drillthrough [Analysis Services]
- drillthrough [DMX]
ms.assetid: 246c784b-1b0c-4f0b-96f7-3af265e67051
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ca74fe9ec36262130e01a58280f9d966c35c3485
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66084547"
---
# <a name="drillthrough-queries-data-mining"></a>Consultas de detalhamento (mineração de dados)
  Uma *consulta de detalhamento* permite que você recupere detalhes de casos subjacentes ou estrutura de dados, enviando uma consulta ao modelo de mineração. O detalhamento é útil se você quiser exibir os casos que foram utilizados para treinar o modelo, versus os casos utilizados para testar o modelo, ou se você quiser ver detalhes adicionais dos dados dos casos.  
  
 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Data Mining fornece duas opções diferentes para detalhamento:  
  
-   Detalhamento para os **casos de modelo**  
  
     O detalhamento para casos de modelo é usado quando você deseja ir de um padrão específico no modelo, como um cluster ou uma ramificação de uma árvore de decisão, e exibir detalhes sobre os casos individuais.  
  
-   Detalhamento para os **casos de estrutura**  
  
     O detalhamento dos casos de estrutura é usado quando a estrutura contém informações que podem não estar disponíveis no modelo. Por exemplo, você não utilizará informações de contato de clientes em um modelo de clustering, mesmo se os dados estiverem inclusos na estrutura. Entretanto, depois que você criar o modelo, talvez queira recuperar as informações de contato para clientes que estão agrupados em um determinado cluster.  
  
 Esta seção fornece exemplos de como você pode criar essas consultas.  
  
 [Usando o detalhamento no designer de mineração de dados](#bkmk_Designer)  
  
 [Criando consultas de detalhamento usando DMX](#bkmk_DMX)  
  
 [Considerações ao usar o detalhamento](#bkmk_Considerations)  
  
-   [Problemas de segurança](#bkmk_Security)  
  
-   [Limitações](#bkmk_Limits)  
  
##  <a name="bkmk_Designer"></a>Usando o detalhamento no designer de mineração de dados  
 Se um modelo de mineração estiver configurado para permitir os detalhamento e se você tiver as permissões adequadas, quando procurar o modelo, poderá clicar em um nó no visualizador apropriado e recuperar informações detalhadas sobre os casos naquele nó específico.  
  
 [Detalhar os dados de caso de um modelo de mineração](drill-through-to-case-data-from-a-mining-model.md).  
  
 Se os casos de treinamento foram colocados no cache durante o processamento da estrutura de mineração e você tem as permissões necessárias, poderá retornar informações dos casos de modelo e da estrutura de mineração, até de colunas que não foram incluídas no modelo de mineração.  
  
##  <a name="bkmk_DMX"></a>Criando consultas de detalhamento usando DMX  
 Você poderá detalhar os dados de caso criando uma consulta DMX caso tenha permissões no modelo ou na estrutura. Para obter exemplos da sintaxe para criar consultas de detalhamento em DMX, consulte o seguinte tópico:  
  
 [Criar consultas de detalhamento usando DMX](create-drillthrough-queries-using-dmx.md)  
  
##  <a name="bkmk_Considerations"></a>Considerações ao usar o detalhamento  
  
-   Se você utilizar o Assistente de Mineração de Dados, a opção para habilitar o detalhamento para os casos de modelos estará na página final do assistente. O detalhamento está desabilitado por padrão. Para obter mais informações, consulte [Concluindo o assistente &#40;Assistente de Mineração de Dados&#41;](../completing-the-wizard-data-mining-wizard.md).  
  
-   Você pode acrescentar a habilidade de detalhamento em um modelo de mineração existente, mas se fizer isso, o modelo deve ser reprocessado antes da análise dos dados.  
  
-   O detalhamento funciona com a recuperação de informações sobre os casos de treinamento armazenados em cache quando você processou a estrutura de mineração. Assim, se você limpou os dados em cache após o processamento da estrutura alterando a propriedade <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> para `ClearAfterProcessing`, o detalhamento não funcionará. Para habilitar o detalhamento para colunas de estrutura, você deve alterar a propriedade <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> para `KeepTrainingCases` e depois processar a estrutura novamente.  
  
-   Se a estrutura de mineração não permitir o detalhamento, mas o modelo de mineração permitir, você poderá exibir informações somente dos casos de modelo e não da estrutura de mineração.  
  
###  <a name="bkmk_Security"></a>Problemas de segurança para detalhamento  
 Se desejar detalhar os casos de estrutura do modelo, você deve verificar se a estrutura de mineração e o modelo de mineração têm a propriedade [AllowDrillThrough](https://docs.microsoft.com/bi-reference/assl/properties/allowdrillthrough-element-assl) definida como `True`. Além disso, você deve ser um membro da função que tem as permissões de detalhamento no modelo e na estrutura. Para obter informações sobre como criar funções, consulte [Designer de Função &#40;Analysis Services – Dados Multidimensionais&#41;](https://msdn.microsoft.com/library/ms189696(v=sql.120).aspx). consulte.  
  
 As permissões de detalhamento são definidas separadamente na estrutura e no modelo. A permissão para o modelo lhe permite detalhar do modelo, mesmo que você não tenha permissões na estrutura. As permissões para detalhamento na estrutura fornecem a capacidade adicional de incluir colunas de estrutura em consultas de detalhamento do modelo, usando a função [StructureColumn &#40;DMX&#41;](/sql/dmx/structurecolumn-dmx).  
  
> [!NOTE]  
>  Se você habilitar o detalhamento na estrutura de mineração e no modelo de mineração, qualquer usuário que for membro de uma função que tenha permissões de análise no modelo de mineração também poderá exibir colunas na estrutura de mineração, até mesmo se essas colunas não estiverem incluídas no modelo de mineração. Portanto, para proteger dados confidenciais, você deve configurar a exibição da fonte de dados para mascarar informações pessoais e só permitir acesso ao detalhamento na estrutura de mineração quando necessário.  
  
###  <a name="bkmk_Limits"></a>Limitações no detalhamento  
  
-   As seguintes limitações se aplicam às operações de detalhamento em um modelo, dependendo do algoritmo que foi utilizado para criar o modelo:  
  
|Nome do algoritmo|Problema|  
|--------------------|-----------|  
|Algoritmo Microsoft Naïve Bayes|Sem suporte. Estes algoritmos não atribuem casos a nós específicos no conteúdo.|  
|Algoritmo Rede Neural da Microsoft|Sem suporte. Estes algoritmos não atribuem casos a nós específicos no conteúdo.|  
|Algoritmo Regressão Logística da Microsoft|Sem suporte. Estes algoritmos não atribuem casos a nós específicos no conteúdo.|  
|Algoritmo Regressão Linear da Microsoft| Com suporte. Porém, como o modelo cria um único nó, `All`, o detalhamento retorna todos os casos de treinamento para o modelo. Se o conjunto de treinamento for grande, o carregamento dos resultados poderá demorar muito tempo.|  
|Algoritmo Microsoft Time Series| Com suporte. Porém, você não pode detalhar a estrutura nem os dados de casos utilizando o **Visualizador de Modelo de Mineração** no Designer de Mineração de Dados. Em vez disso, você deve criar uma consulta DMX.<br /><br /> Além disso, você não pode detalhar nós específicos nem gravar uma consulta DMX para recuperar casos em nós específicos do modelo Time Series. Você pode recuperar dados de casos a partir da redução do modelo ou da estrutura utilizando outros critérios, como valores data ou de atributo.<br /><br /> Você também pode retornar as datas dos casos no modelo, usando a função [Lag &#40;DMX&#41;](/sql/dmx/lag-dmx).<br /><br /> Se você quiser ver detalhes dos nós ARTXP e ARIMA criados pelo algoritmo MTS, poderá utilizar o [Visualizador de Árvore de Conteúdo Genérico da Microsoft &#40;Mineração de dados&#41;](../microsoft-generic-content-tree-viewer-data-mining.md).|  
  
##  <a name="bkmk_Tasks"></a> Tarefas relacionadas  
 Use os links a seguir para trabalhar com detalhamento em cenários específicos.  
  
|Tarefa|Link|  
|----------|----------|  
|O procedimento que descreve o uso de detalhamento no Designer de Mineração de Dados|[Detalhar dados do caso a partir do modelo de mineração](drill-through-to-case-data-from-a-mining-model.md)|  
|Para alterar um modelo de mineração existente para permitir detalhamento|[Habilitar o detalhamento para um modelo de mineração](enable-drillthrough-for-a-mining-model.md)|  
|Permitindo detalhamento em uma estrutura de mineração usando a cláusula DMX WITH DRILLTHROUGH|[CRIAR ESTRUTURA DE MINERAÇÃO &#40;&#41;DMX](/sql/dmx/create-mining-structure-dmx)|  
|Para obter informações sobre como atribuir permissões que se aplicam a detalhamento em estruturas de mineração e modelos de mineração|[Conceder permissões em estruturas e modelos de Data Mining &#40;Analysis Services&#41;](../multidimensional-models/grant-permissions-on-data-mining-structures-and-models-analysis-services.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Visualizadores de modelo de mineração de dados](data-mining-model-viewers.md)   
 [Consultas de mineração de dados](data-mining-queries.md)  
  
  
