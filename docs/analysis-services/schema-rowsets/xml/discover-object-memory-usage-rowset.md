---
title: Conjunto de linhas DISCOVER_OBJECT_MEMORY_USAGE | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: bcff047c859bf4e26de8143ed7efef93b8f62e29
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="discoverobjectmemoryusage-rowset"></a>Conjunto de linhas DISCOVER_OBJECT_MEMORY_USAGE
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Oferece informações sobre recursos de memória usados por objetos.  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O conjunto de linhas **DISCOVER_OBJECT_MEMORY_USAGE** contém as colunas a seguir.  
  
|Nome da coluna|Indicador de tipo|Comprimento|Description|  
|-----------------|--------------------|------------|-----------------|  
|**OBJECT_PARENT_PATH**|**DBTYPE_WSTR**||O caminho para o pai do objeto atual.|  
|**OBJECT_ID**|**DBTYPE_WSTR**||A ID do objeto como definida na hora de criação.|  
|**OBJECT_MEMORY_SHRINKABLE**|**DBTYPE_I8**||A quantidade total de memória (bytes) usada para todos os objetos reduzíveis que são de propriedade direta do objeto atual. O valor atual não inclui memória de objetos pertencentes aos objetos nomeados dos quais o objeto atual é o proprietário direto.|  
|**OBJECT_MEMORY_NONSHRINKABLE**|**DBTYPE_I8**||A quantidade total de memória (bytes) de todos os objetos não reduzíveis que são de propriedade direta do objeto atual. O valor atual não inclui memória de objetos pertencentes aos objetos nomeados dos quais o objeto atual é o proprietário direto.|  
|**OBJECT_VERSION**|**DBTYPE_I4**||O número de versão de metadados do objeto. Esse número mudará sempre que o objeto for alterado.|  
|**OBJECT_DATA_VERSION**|**DBTYPE_I4**||O número de linhagem dos dados do objeto. Esse número será incrementado sempre que o objeto for processado.|  
|**OBJECT_TYPE_ID**|**DBTYPE_I4**||Reservado para uso interno.|  
|**OBJECT_TIME_CREATED**|**DBTYPE_DBTIMESTAMP**||A hora do servidor UTC no momento em que o objeto foi criado.|  
  
 Este conjunto de linhas do esquema não é classificado.  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O conjunto de linhas **DISCOVER_OBJECT_MEMORY_USAGE** pode ser restringido nas colunas listadas na tabela a seguir.  
  
|Nome da coluna|Indicador de tipo|Estado de restrição|  
|-----------------|--------------------|-----------------------|  
|**OBJECT_PARENT_PATH**|**DBTYPE_WSTR**|Opcional.|  
|**OBJECT_ID**|**DBTYPE_WSTR**|Opcional|  
  
## <a name="see-also"></a>Consulte também  
 [XML for Analysis conjuntos de linhas de esquema](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
