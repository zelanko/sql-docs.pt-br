---
title: Conjunto de linhas DMSCHEMA_MINING_FUNCTIONS | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: DMSCHEMA_MINING_FUNCTIONS
apitype: NA
applies_to: SQL Server 2016 Preview
helpviewer_keywords: DMSCHEMA_MINING_FUNCTIONS rowset
ms.assetid: 9ace7493-a7b1-45ca-93de-3cb2f3597017
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: d66ead0b5d3266ed00780d079fdc2f1d78149f50
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="dmschemaminingfunctions-rowset"></a>Conjunto de linhas DMSCHEMA_MINING_FUNCTIONS
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Descreve as funções de mineração de dados que são suportadas por algoritmos de mineração de dados disponíveis em um servidor que esteja executando [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O **DMSCHEMA_MINING_FUNCTIONS** linhas contém as seguintes colunas.  
  
|Nome da coluna|Indicador de tipo|Comprimento|Description|  
|-----------------|--------------------|------------|-----------------|  
|**SERVICE_NAME**|**DBTYPE_WSTR**||O nome do algoritmo.|  
|**NOME_DA_FUNÇÃO**|**DBTYPE_WSTR**||O nome da função.|  
|**FUNCTION_SIGNATURE**|**DBTYPE_WSTR**||A assinatura da função.|  
|**RETURNS_TABLE**|**DBTYPE_BOOL**||**FALSE** se a função retornar conteúdo escalar (como o comprimento do argumento caracteres); **TRUE** se a função retorna uma tabela (como uma tabela de histograma).|  
|**DESCRIPTION**|**DBTYPE_WSTR**||Uma descrição amigável da função.|  
|**HELP_FILE**|**DBTYPE_WSTR**||O nome do arquivo que contém a documentação desta função.|  
|**HELP_CONTEXT**|**DBTYPE_I4**||A ID de contexto da Ajuda para esta função.|  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O **DMSCHEMA_MINING_FUNCTIONS** linhas pode ser restringido nas colunas listadas na tabela a seguir.  
  
|Nome da coluna|Indicador de tipo|Estado de restrição|  
|-----------------|--------------------|-----------------------|  
|**SERVICE_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**NOME_DA_FUNÇÃO**|**DBTYPE_WSTR**|Opcional.|  
  
## <a name="see-also"></a>Consulte Também  
 [Conjuntos de linhas de esquema de mineração de dados](../../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
  
