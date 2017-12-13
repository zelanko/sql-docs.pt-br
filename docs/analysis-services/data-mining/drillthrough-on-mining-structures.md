---
title: "Detalhamento em estruturas de mineração | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a0b00a3b-f9db-4289-a8cb-ddf600cd64ac
caps.latest.revision: "6"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 96d9e924f914822b7eb26b4242c1120113da7c3b
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="drillthrough-on-mining-structures"></a>Detalhamento em estruturas de mineração
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]*Detalhamento* significa ter a capacidade de consultar um modelo de mineração ou uma estrutura de mineração e obter dados detalhados não exposta no modelo.  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] oferece duas opções diferentes de detalhamento em dados de caso. Você pode detalhar para os dados que foram usados para criar o modelo de mineração ou pode detalhar para os dados de origem na estrutura de mineração.  
  
## <a name="drillthrough-to-model-cases-vs-drillthrough-to-structure"></a>Detalhar para casos do modelo vs. Detalhar para estrutura  
 O detalhamento para **casos do modelo** é útil para localizar detalhes adicionais sobre regras, padrões ou clusters em um modelo.  
  
 Em contraste, os dados **detalhamento para estrutura** visam fornecer acesso a informações que não foram disponibilizadas no modelo. Por exemplo, se você tem as permissões adequadas, talvez queira descobrir quais linhas de dados foram usadas para treinar o modelo e quais foram usadas para testes.  
  
 Você também pode exibir atributos dos dados que não foram usados na análise, desde que eles tenham sido incluídos na definição de estrutura. Por exemplo, muitas vezes as estruturas de mineração oferecem suporte a vários tipos diferentes de modelos; algumas colunas de estrutura podem ter sido excluídas de um modelo porque o tipo de dados era incompatível ou os dados não eram úteis para a análise. Por exemplo, você não usaria informações de contato de cliente em um modelo de clustering, mesmo que os dados fossem incluídos na estrutura, mas, ao habilitar o detalhamento, você ganha acesso a essas informações sem executar consultas separadas na fonte de dados.  
  
## <a name="enabling-drillthrough-to-structure-data"></a>Habilitando o detalhamento para estruturar dados  
 Para usar o detalhamento na estrutura de mineração, as seguintes condições precisam ser atendidas:  
  
-   O detalhamento no modelo também deve ser habilitado. Por padrão, o detalhamento dos dois tipos é desabilitado. Para habilitar o detalhamento no Assistente de Mineração de Dados, selecione a opção para habilitar o detalhamento para casos do modelo na página final do assistente. Também é possível adicionar a capacidade de detalhar em um modelo posteriormente, alterando a propriedade **AllowDrillthrough** .  
  
-   Se você criar a estrutura de mineração usando DMX, use a cláusula WITH DRILLTHROUGH. Para obter mais informações, consulte [CREATE MINING STRUCTURE &#40;DMX&#41;](../../dmx/create-mining-structure-dmx.md).  
  
-   O detalhamento funciona com a recuperação de informações sobre os casos de treinamento armazenados em cache quando você processou a estrutura de mineração. Assim, se você optar por limpar todos os dados em cache após processar a estrutura alterando a propriedade <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> para **ClearAfterProcessing**, o detalhamento não funcionará. Para habilitar o detalhamento em colunas de estrutura, é necessário alterar a propriedade <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> para **KeepTrainingCases** e processar a estrutura novamente.  
  
-   Verifique se a estrutura de mineração e o modelo de mineração têm a propriedade [AllowDrillThrough](../../analysis-services/scripting/properties/allowdrillthrough-element-assl.md) definida como **True**. Além disso, você deve ser um membro da função que tem as permissões de detalhamento no modelo e na estrutura.  
  
## <a name="security-issues-for-drillthrough"></a>Problemas de segurança para detalhamento  
 As permissões de detalhamento são definidas separadamente na estrutura e no modelo. A permissão para o modelo lhe permite detalhar do modelo, mesmo que você não tenha permissões na estrutura. As permissões para detalhamento na estrutura fornecem a capacidade adicional de incluir colunas de estrutura em consultas de detalhamento do modelo, usando a função [StructureColumn &#40;DMX&#41;](../../dmx/structurecolumn-dmx.md).  
  
 Para obter informações sobre como criar funções e atribuir permissões no Analysis Services, consulte [Designer de Função &#40;Analysis Services – Dados Multidimensionais&#41;](http://msdn.microsoft.com/library/e8ba42db-0565-4d68-b3ab-0c63d8d07192).  
  
> [!NOTE]  
>  Se você habilitar o detalhamento na estrutura de mineração e no modelo de mineração, qualquer usuário que for membro de uma função que tenha permissões de análise no modelo de mineração também poderá exibir colunas na estrutura de mineração, até mesmo se essas colunas não estiverem incluídas no modelo de mineração. Portanto, para proteger dados confidenciais, você deve configurar a exibição da fonte de dados para mascarar informações pessoais e só permitir acesso ao detalhamento na estrutura de mineração quando necessário.  
  
## <a name="related-tasks"></a>Tarefas relacionadas  
 Consulte os tópicos a seguir para obter mais informações sobre como usar o detalhamento com modelos de mineração.  
  
|||  
|-|-|  
|Use o detalhamento para estruturar a partir de visualizadores do modelo de mineração|[Usar detalhamento dos visualizadores do modelo](../../analysis-services/data-mining/use-drillthrough-from-the-model-viewers.md)|  
|Veja exemplos de consultas de detalhamento para tipos de modelo específicos.|[Consultas de mineração de dados](../../analysis-services/data-mining/data-mining-queries.md)|  
|Obtenha informações sobre permissões que se aplicam a estruturas de mineração e modelos de mineração específicos.|[Conceder permissões em estruturas e modelos de mineração de dados &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-permissions-on-data-mining-structures-and-models-analysis-services.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Detalhamento em modelos de mineração](../../analysis-services/data-mining/drillthrough-on-mining-models.md)  
  
  
