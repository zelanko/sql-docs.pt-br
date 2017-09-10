---
title: "Conjuntos de linhas do esquema de mineração de dados | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- schema rowsets [Analysis Services], data mining
- schema rowsets [Analysis Services]
- rowsets [Analysis Services], data mining
- data mining [Analysis Services], schema rowsets
ms.assetid: bd7d5df5-500b-4159-8467-880e141bc043
caps.latest.revision: 44
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ad8ac453d1d299be98f3cb46496685063fd66576
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="data-mining-schema-rowsets"></a>Conjuntos de linhas de esquema de mineração de dados
  Um servidor que está executando [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] suporta os seguintes conjuntos de linhas do esquema de mineração de dados. Para verificar se um determinado provedor XML/A oferece suporte a um conjunto de linhas específico, use o [DISCOVER_ENUMERATORS](../../../analysis-services/schema-rowsets/xml/discover-enumerators-rowset.md) conjunto de linhas com o [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) método.  
  
 No [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], os conjuntos de linhas de esquema de mineração de dados são exibidos como tabelas na linguagem Transact-SQL, no esquema $SYSTEM. Por exemplo, a consulta a seguir, feita em uma instância do Analysis Services, retorna uma lista dos esquemas disponíveis na instância atual.  
  
```  
SELECT * FROM [$system].[DBSCHEMA_TABLES]  
```  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Conjunto de linhas do esquema|Description|  
|-------------------|-----------------|  
|[Linhas de DMSCHEMA_MINING_COLUMNS](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-columns-rowset.md)|Descreve as colunas individuais de todos os modelos de mineração de dados definidos implantados no servidor.|  
|[Conjunto de linhas DMSCHEMA_MINING_FUNCTIONS](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-functions-rowset.md)|Descreve as funções de previsão e as funções de mineração que podem ser usadas com cada algoritmo de mineração de dados instalado no servidor.|  
|[Conjunto de linhas DMSCHEMA_MINING_MODEL_CONTENT](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-model-content-rowset.md)|Permite que o aplicativo cliente procure o conteúdo de um modelo de mineração de dados treinado.|  
|[Conjunto de linhas DMSCHEMA_MINING_MODEL_CONTENT_PMML](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-model-content-pmml-rowset.md)|Retorna a representação XML (PMML 2.1) do conteúdo do modelo de mineração.|  
|[Conjunto de linhas DMSCHEMA_MINING_MODEL_XML](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-model-xml-rowset.md)|Retorna a estrutura XML (PMML 2.1) do modelo de mineração. Este é o mesmo esquema de DMSCHEMA_MINING_MODEL_PMML, preservado para compatibilidade com versões anteriores.|  
|[Conjunto de linhas DMSCHEMA_MINING_MODELS](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-models-rowset.md)|Enumera os modelos de mineração de dados implantados no servidor.|  
|[Conjunto de linhas DMSCHEMA_MINING_SERVICE_PARAMETERS](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-service-parameters-rowset.md)|Oferece uma lista de parâmetros que podem ser usados na configuração do comportamento de cada algoritmo de mineração de dados instalado no servidor.|  
|[Conjunto de linhas DMSCHEMA_MINING_SERVICES](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-services-rowset.md)|Oferece uma descrição de cada algoritmo de mineração de dados disponível no servidor.|  
|[Conjunto de linhas DMSCHEMA_MINING_STRUCTURE_COLUMNS](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-structure-columns-rowset.md)|Descreve as colunas individuais de todas as estruturas de mineração implantadas no servidor.|  
|[Conjunto de linhas DMSCHEMA_MINING_STRUCTURES](../../../analysis-services/schema-rowsets/data-mining/dmschema-mining-structures-rowset.md)|Enumera informações sobre estruturas de mineração.|  
  
 Todas as linhas do esquema listadas aqui são suportadas pelo servidor que está executando [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [Conjuntos de linhas do esquema do Analysis Services](../../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)   
 [Linhas do esquema de mineração de dados &#40; SSAs &#41;](../../../analysis-services/data-mining/data-mining-schema-rowsets-ssas.md)  
  
  
