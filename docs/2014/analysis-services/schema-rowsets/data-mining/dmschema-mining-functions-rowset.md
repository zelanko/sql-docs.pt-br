---
title: Conjunto de linhas DMSCHEMA_MINING_FUNCTIONS | Microsoft Docs
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
api_name:
- DMSCHEMA_MINING_FUNCTIONS
topic_type:
- apiref
helpviewer_keywords:
- DMSCHEMA_MINING_FUNCTIONS rowset
ms.assetid: 9ace7493-a7b1-45ca-93de-3cb2f3597017
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: b5a60e18a57c15976e7a7bd5d5e31729e255869a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36120227"
---
# <a name="dmschemaminingfunctions-rowset"></a>Conjunto de linhas DMSCHEMA_MINING_FUNCTIONS
  Descreve as funções de mineração de dados que são suportadas por algoritmos de mineração de dados disponíveis em um servidor que esteja executando [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O `DMSCHEMA_MINING_FUNCTIONS` linhas contém as seguintes colunas.  
  
|Nome da coluna|Indicador de tipo|Comprimento|Description|  
|-----------------|--------------------|------------|-----------------|  
|`SERVICE_NAME`|`DBTYPE_WSTR`||O nome do algoritmo.|  
|`FUNCTION_NAME`|`DBTYPE_WSTR`||O nome da função.|  
|`FUNCTION_SIGNATURE`|`DBTYPE_WSTR`||A assinatura da função.|  
|`RETURNS_TABLE`|`DBTYPE_BOOL`||`FALSE` se a função retornar conteúdo escalar (como o comprimento do argumento do caractere); `TRUE` se a função retornar uma tabela (como uma tabela de histograma).|  
|`DESCRIPTION`|`DBTYPE_WSTR`||Uma descrição amigável da função.|  
|`HELP_FILE`|`DBTYPE_WSTR`||O nome do arquivo que contém a documentação desta função.|  
|`HELP_CONTEXT`|`DBTYPE_I4`||A ID de contexto da Ajuda para esta função.|  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O conjunto de linhas `DMSCHEMA_MINING_FUNCTIONS` pode ser restringido nas colunas listadas na tabela a seguir.  
  
|Nome da coluna|Indicador de tipo|Estado de restrição|  
|-----------------|--------------------|-----------------------|  
|`SERVICE_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`FUNCTION_NAME`|`DBTYPE_WSTR`|Opcional.|  
  
## <a name="see-also"></a>Consulte também  
 [Conjuntos de linhas de esquema de mineração de dados](../../schema-rowsets/data-mining/data-mining-schema-rowsets.md) 
  
  