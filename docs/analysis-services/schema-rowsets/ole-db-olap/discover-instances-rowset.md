---
title: Conjunto de linhas DISCOVER_INSTANCES | Microsoft Docs
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
apiname:
- DISCOVER_INSTANCES
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DISCOVER_INSTANCES rowset
ms.assetid: e0842e63-089d-468d-869f-634da343d9fb
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: fbed6de71f83da959591003039fe5910a1a4c53d
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="discoverinstances-rowset"></a>Conjunto de linhas DISCOVER_INSTANCES
  Descreve as instâncias no servidor.  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O conjunto de linhas **DISCOVER_INSTANCES** contém as colunas a seguir.  
  
|Nome da coluna|Indicador de tipo|Comprimento|Description|  
|-----------------|--------------------|------------|-----------------|  
|**NOME_DA_INSTÂNCIA**|**DBTYPE_WSTR**||O nome da instância.|  
|**INSTANCE_PORT_NUMBER**|**DBTYPE_I4**||O número da porta na qual a instância escuta.|  
|**INSTANCE_STATE**|**DBTYPE_I4**||O estado da instância do servidor:<br /><br /> **Introdução**<br /><br /> **Stopped (parado)**<br /><br /> **Iniciando**<br /><br /> **Parando**<br /><br /> **Em Pausa**|  
  
 Este conjunto de linhas do esquema não é classificado.  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O conjunto de linhas **DISCOVER_INSTANCES** pode ser restringido nas colunas listadas na tabela a seguir.  
  
|Nome da coluna|Indicador de tipo|Estado de restrição|  
|-----------------|--------------------|-----------------------|  
|**NOME_DA_INSTÂNCIA**|**DBTYPE_WSTR**|Opcional.|  
  
## <a name="see-also"></a>Consulte também  
 [OLE DB para OLAP Schema Rowsets](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  

