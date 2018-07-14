---
title: Detalhamento em estruturas de mineração | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: a0b00a3b-f9db-4289-a8cb-ddf600cd64ac
caps.latest.revision: 6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4e01f903d28368179a7c249f3a8bbb7ac7c159e8
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37246086"
---
# <a name="drillthrough-on-mining-structures"></a>Detalhamento em estruturas de mineração
  *Detalhar* significa ter a capacidade de consultar um modelo de mineração ou uma estrutura de mineração e obter dados detalhados não expostos no modelo.  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] oferece duas opções diferentes de detalhamento em dados de caso. Você pode detalhar para os dados que foram usados para criar o modelo de mineração ou pode detalhar para os dados de origem na estrutura de mineração.  
  
## <a name="drillthrough-to-model-cases-vs-drillthrough-to-structure"></a>Detalhar para casos do modelo vs. Detalhar para estrutura  
 O detalhamento para **casos do modelo** é útil para localizar detalhes adicionais sobre regras, padrões ou clusters em um modelo.  
  
 Em contraste, os dados **detalhamento para estrutura** visam fornecer acesso a informações que não foram disponibilizadas no modelo. Por exemplo, se você tem as permissões adequadas, talvez queira descobrir quais linhas de dados foram usadas para treinar o modelo e quais foram usadas para testes.  
  
 Você também pode exibir atributos dos dados que não foram usados na análise, desde que eles tenham sido incluídos na definição de estrutura. Por exemplo, muitas vezes as estruturas de mineração oferecem suporte a vários tipos diferentes de modelos; algumas colunas de estrutura podem ter sido excluídas de um modelo porque o tipo de dados era incompatível ou os dados não eram úteis para a análise. Por exemplo, você não usaria informações de contato de cliente em um modelo de clustering, mesmo que os dados fossem incluídos na estrutura, mas, ao habilitar o detalhamento, você ganha acesso a essas informações sem executar consultas separadas na fonte de dados.  
  
## <a name="enabling-drillthrough-to-structure-data"></a>Habilitando o detalhamento para estruturar dados  
 Para usar o detalhamento na estrutura de mineração, as seguintes condições precisam ser atendidas:  
  
-   O detalhamento no modelo também deve ser habilitado. Por padrão, o detalhamento dos dois tipos é desabilitado. Para habilitar o detalhamento no Assistente de Mineração de Dados, selecione a opção para habilitar o detalhamento para casos do modelo na página final do assistente. Você também pode adicionar a capacidade de detalhamento em um modelo posteriormente, alterando o `AllowDrillthrough` propriedade.  
  
-   Se você criar a estrutura de mineração usando DMX, use a cláusula WITH DRILLTHROUGH. Para obter mais informações, consulte [CREATE MINING STRUCTURE &#40;DMX&#41;](/sql/dmx/create-mining-structure-dmx).  
  
-   O detalhamento funciona com a recuperação de informações sobre os casos de treinamento armazenados em cache quando você processou a estrutura de mineração. Portanto, se você limpar os dados armazenados em cache após processar a estrutura alterando a <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> propriedade para `ClearAfterProcessing`, detalhamento não funcionará. Para habilitar o detalhamento para colunas de estrutura, você deve alterar o <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> propriedade para `KeepTrainingCases` e, em seguida, reprocessar a estrutura.  
  
-   Verifique se a estrutura de mineração e o modelo de mineração tem o [AllowDrillThrough](../scripting/properties/allowdrillthrough-element-assl.md) propriedade definida como `True`. Além disso, você deve ser um membro da função que tem as permissões de detalhamento no modelo e na estrutura.  
  
## <a name="security-issues-for-drillthrough"></a>Problemas de segurança para detalhamento  
 As permissões de detalhamento são definidas separadamente na estrutura e no modelo. A permissão para o modelo lhe permite detalhar do modelo, mesmo que você não tenha permissões na estrutura. As permissões para detalhamento na estrutura fornecem a capacidade adicional de incluir colunas de estrutura em consultas de detalhamento do modelo, usando a função [StructureColumn &#40;DMX&#41;](/sql/dmx/structurecolumn-dmx).  
  
 Para obter informações sobre como criar funções e atribuir permissões no Analysis Services, consulte [Designer de Função &#40;Analysis Services – Dados Multidimensionais&#41;](https://msdn.microsoft.com/library/ms189696(v=sql.120).aspx).  
  
> [!NOTE]  
>  Se você habilitar o detalhamento na estrutura de mineração e no modelo de mineração, qualquer usuário que for membro de uma função que tenha permissões de análise no modelo de mineração também poderá exibir colunas na estrutura de mineração, até mesmo se essas colunas não estiverem incluídas no modelo de mineração. Portanto, para proteger dados confidenciais, você deve configurar a exibição da fonte de dados para mascarar informações pessoais e só permitir acesso ao detalhamento na estrutura de mineração quando necessário.  
  
## <a name="related-tasks"></a>Related Tasks  
 Consulte os tópicos a seguir para obter mais informações sobre como usar o detalhamento com modelos de mineração.  
  
|||  
|-|-|  
|Use o detalhamento para estruturar a partir de visualizadores do modelo de mineração|[Usar detalhamento dos visualizadores do modelo](use-drillthrough-from-the-model-viewers.md)|  
|Veja exemplos de consultas de detalhamento para tipos de modelo específicos.|[Consultas de mineração de dados](data-mining-queries.md)|  
|Obtenha informações sobre permissões que se aplicam a estruturas de mineração e modelos de mineração específicos.|[Conceder permissões em estruturas de mineração de dados e modelos de &#40;Analysis Services&#41;](../multidimensional-models/grant-permissions-on-data-mining-structures-and-models-analysis-services.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Detalhamento em modelos de mineração](drillthrough-on-mining-models.md)  
  
  
