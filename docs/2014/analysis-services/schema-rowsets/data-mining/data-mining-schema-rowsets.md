---
title: Conjuntos de linhas do esquema de mineração de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
- apinav
helpviewer_keywords:
- schema rowsets [Analysis Services], data mining
- schema rowsets [Analysis Services]
- rowsets [Analysis Services], data mining
- data mining [Analysis Services], schema rowsets
ms.assetid: bd7d5df5-500b-4159-8467-880e141bc043
caps.latest.revision: 43
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 9302e8dbafd31f4efb3b053ea5247f2b860dc8bc
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36011489"
---
# <a name="data-mining-schema-rowsets"></a>Conjuntos de linhas de esquema de mineração de dados
  Um servidor que está executando [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] suporta os seguintes conjuntos de linhas do esquema de mineração de dados. Para verificar se um determinado provedor XML/A oferece suporte a um conjunto de linhas específico, use o [DISCOVER_ENUMERATORS](../xml/discover-enumerators-rowset.md) conjunto de linhas com o [Discover](../../xmla/xml-elements-methods-discover.md) método.  
  
 No [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], os conjuntos de linhas de esquema de mineração de dados são exibidos como tabelas na linguagem Transact-SQL, no esquema $SYSTEM. Por exemplo, a consulta a seguir, feita em uma instância do Analysis Services, retorna uma lista dos esquemas disponíveis na instância atual.  
  
```  
SELECT * FROM [$system].[DBSCHEMA_TABLES]  
```  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Conjunto de linhas do esquema|Description|  
|-------------------|-----------------|  
|[Conjunto de linhas DMSCHEMA_MINING_COLUMNS](dmschema-mining-columns-rowset.md)|Descreve as colunas individuais de todos os modelos de mineração de dados definidos implantados no servidor.|  
|[Conjunto de linhas DMSCHEMA_MINING_FUNCTIONS](dmschema-mining-functions-rowset.md)|Descreve as funções de previsão e as funções de mineração que podem ser usadas com cada algoritmo de mineração de dados instalado no servidor.|  
|[Conjunto de linhas DMSCHEMA_MINING_MODEL_CONTENT](dmschema-mining-model-content-rowset.md)|Permite que o aplicativo cliente procure o conteúdo de um modelo de mineração de dados treinado.|  
|[Conjunto de linhas DMSCHEMA_MINING_MODEL_CONTENT_PMML](dmschema-mining-model-content-pmml-rowset.md)|Retorna a representação XML (PMML 2.1) do conteúdo do modelo de mineração.|  
|[Conjunto de linhas DMSCHEMA_MINING_MODEL_XML](dmschema-mining-model-xml-rowset.md)|Retorna a estrutura XML (PMML 2.1) do modelo de mineração. Este é o mesmo esquema de DMSCHEMA_MINING_MODEL_PMML, preservado para compatibilidade com versões anteriores.|  
|[Conjunto de linhas DMSCHEMA_MINING_MODELS](dmschema-mining-models-rowset.md)|Enumera os modelos de mineração de dados implantados no servidor.|  
|[Conjunto de linhas DMSCHEMA_MINING_SERVICE_PARAMETERS](dmschema-mining-service-parameters-rowset.md)|Oferece uma lista de parâmetros que podem ser usados na configuração do comportamento de cada algoritmo de mineração de dados instalado no servidor.|  
|[Conjunto de linhas DMSCHEMA_MINING_SERVICES](dmschema-mining-services-rowset.md)|Oferece uma descrição de cada algoritmo de mineração de dados disponível no servidor.|  
|[Conjunto de linhas DMSCHEMA_MINING_STRUCTURE_COLUMNS](dmschema-mining-structure-columns-rowset.md)|Descreve as colunas individuais de todas as estruturas de mineração implantadas no servidor.|  
|[Conjunto de linhas DMSCHEMA_MINING_STRUCTURES](dmschema-mining-structures-rowset.md)|Enumera informações sobre estruturas de mineração.|  
  
 Todas as linhas do esquema listadas aqui são suportadas pelo servidor que está executando [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [Conjuntos de linhas do esquema do Analysis Services](../../schema-rowsets/analysis-services-schema-rowsets.md)   
 [Consultando o catálogo de sistema do SQL Server](https://technet.microsoft.com/en-us/library/ms189082\(v=sql.110\).aspx)   
 [Consultando os conjuntos de linhas do esquema de mineração de dados &#40;Analysis Services – mineração de dados&#41;](../../data-mining/data-mining-schema-rowsets-ssas.md)  
  
  