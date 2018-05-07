---
title: Conjunto de linhas DISCOVER_INSTANCES | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4143aa33cc4c09914ffb05aaccbb12f2fe64d440
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="discoverinstances-rowset"></a>Conjunto de linhas DISCOVER_INSTANCES
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
  
  
