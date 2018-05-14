---
title: Conjuntos de linhas do esquema de mineração de dados | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0324ee3b35f4b45162b9646d2d0e9cfeada47551
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="data-mining-schema-rowsets"></a>Conjuntos de linhas de esquema de mineração de dados
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
 [Conjuntos de linhas do esquema de mineração de dados &#40;SSAs&#41;](../../../analysis-services/data-mining/data-mining-schema-rowsets-ssas.md)  
  
  
