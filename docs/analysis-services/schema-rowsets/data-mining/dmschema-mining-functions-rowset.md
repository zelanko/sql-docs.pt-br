---
title: Conjunto de linhas DMSCHEMA_MINING_FUNCTIONS | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d069e944aeed7d2f49ad30fda3402d8f50cb1cd5
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34027716"
---
# <a name="dmschemaminingfunctions-rowset"></a>Conjunto de linhas DMSCHEMA_MINING_FUNCTIONS
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Descreve as funções de mineração de dados que são suportadas por algoritmos de mineração de dados disponíveis em um servidor que esteja executando [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Linhas do esquema de mineração de dados](../../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
  
