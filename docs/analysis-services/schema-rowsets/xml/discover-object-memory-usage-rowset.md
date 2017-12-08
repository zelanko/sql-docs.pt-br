---
title: Conjunto de linhas DISCOVER_OBJECT_MEMORY_USAGE | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: schema-rowsets
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords: DISCOVER_OBJECT_MEMORY_USAGE rowset
ms.assetid: 211cfa04-7bd6-43fe-8bd5-bfbff78bdafb
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 1a312ed6538be5e639283ade4f77a848ed6e9893
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="discoverobjectmemoryusage-rowset"></a>Conjunto de linhas DISCOVER_OBJECT_MEMORY_USAGE
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
 [Conjunto de linhas de esquema do XML](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
