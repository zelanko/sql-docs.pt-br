---
title: Conjunto de linhas MDSCHEMA_SETS | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- MDSCHEMA_SETS
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- MDSCHEMA_SETS rowset
ms.assetid: abb00dc0-2b83-48d6-b2ba-6615c1488d06
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4820c18992da2aab0ac8e0550a5cadd75ca193bc
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="mdschemasets-rowset"></a>Conjunto de linhas MDSCHEMA_SETS
  Descreve qualquer conjunto definido atualmente em um banco de dados, incluindo conjuntos do escopo da sessão.  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O **MDSCHEMA_SETS** linhas contém as seguintes colunas.  
  
|Nome da coluna|Indicador de tipo|Description|  
|-----------------|--------------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|O nome do banco de dados.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|Sem suporte.|  
|**CUBE_NAME**|**DBTYPE_WSTR**|O nome do cubo.|  
|**SET_NAME**|**DBTYPE_WSTR**|O nome do conjunto, conforme especificado no **CREATE SET** instrução.|  
|**ESCOPO**|**DBTYPE_I4**|O escopo do conjunto:<br /><br /> **MDSET_SCOPE_GLOBAL** (**1**)<br /><br /> **MDSET_SCOPE_SESSION** (**2**)|  
|**DESCRIPTION**|**DBTYPE_WSTR**|Sem suporte.|  
|**EXPRESSÃO**|**DBTYPE_WSTR**|A expressão para o conjunto.|  
|**DIMENSÕES**|**DBTYPE_WSTR**|Uma lista de hierarquias delimitada por vírgulas incluída no conjunto.|  
|**SET_CAPTION**|**DBTYPE_WSTR**|Um rótulo ou legenda associado ao conjunto. O rótulo ou legenda é usado principalmente para fins de exibição.|  
|**SET_DISPLAY_FOLDER**|**DBTYPE_WSTR**|Uma cadeia de caracteres que identifica o caminho da pasta de exibição que o aplicativo cliente usa para mostrar o conjunto. O separador de nível de pasta é definido pelo aplicativo cliente. Para ferramentas e clientes fornecidos pelo [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], a barra invertida (\\) é o separador de nível. Para fornecer várias pastas de exibição, use um ponto e vírgula (;) para separar as pastas.|  
|**SET_EVALUATION_CONTEXT**|**DBTYPE_I4**|O contexto para o conjunto. O conjunto pode ser estático ou dinâmico. Esta coluna pode ter um dos seguintes valores:<br /><br /> MDSET_RESOLUTION_STATIC=1<br /><br /> MDSET_RESOLUTION_DYNAMIC=2|  
  
 O conjunto de linhas é classificado em **CATALOG_NAME**, **SCHEMA_NAME**, **CUBE_NAME**.  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O **MDSCHEMA_SETS** linhas pode ser restringido nas colunas listadas na tabela a seguir.  
  
|Nome da coluna|Indicador de tipo|Estado de restrição|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**CUBE_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**SET_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**ESCOPO**|**DBTYPE_I4**|Opcional.|  
|**HIERARCHY_UNIQUE_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**CUBE_SOURCE**|**DBTYPE_UI2**|Opcional.<br /><br /> Observação: Somente uma hierarquia pode ser incluída e só os conjuntos nomeados cujas hierarquias correspondam exatamente à restrição serão retornados.|  
  
## <a name="see-also"></a>Consulte também  
 [OLE DB para OLAP Schema Rowsets](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  

