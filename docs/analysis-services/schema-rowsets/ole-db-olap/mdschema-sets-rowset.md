---
title: Conjunto de linhas MDSCHEMA_SETS | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 666f8aa8889f2d15e9e62499e41ad9c0bc69fcff
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="mdschemasets-rowset"></a>Conjunto de linhas MDSCHEMA_SETS
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
  
  
