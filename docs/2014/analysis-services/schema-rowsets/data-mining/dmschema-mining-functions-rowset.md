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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3b726c81df5a6085ee52b177d95b4917d7cb8be1
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37169637"
---
# <a name="dmschemaminingfunctions-rowset"></a>Conjunto de linhas DMSCHEMA_MINING_FUNCTIONS
  Descreve as funções de mineração de dados que são compatíveis com os algoritmos de mineração de dados disponíveis em um servidor que está executando [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O `DMSCHEMA_MINING_FUNCTIONS` linhas contém as colunas a seguir.  
  
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
  
  
