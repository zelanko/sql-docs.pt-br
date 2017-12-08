---
title: Conjunto de linhas MDSCHEMA_MEMBERS | Microsoft Docs
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
apiname: MDSCHEMA_MEMBERS
apitype: NA
applies_to: SQL Server 2016 Preview
helpviewer_keywords: MDSCHEMA_MEMBERS rowset
ms.assetid: 0b1aada0-67f8-4ef6-81b2-0100b65e0c2f
caps.latest.revision: "36"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: a5ac98919c5ac10900eb69c9fe7319c6e8b22a75
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="mdschemamembers-rowset"></a>Conjunto de linhas MDSCHEMA_MEMBERS
  Descreve os membros dentro de um banco de dados.  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O **MDSCHEMA_MEMBERS** linhas contém as seguintes colunas.  
  
|Nome da coluna|Indicador de tipo|Comprimento|Description|  
|-----------------|--------------------|------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**||O nome do banco de dados ao qual este membro pertence.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**||O nome do esquema ao qual este membro pertence.|  
|**CUBE_NAME**|**DBTYPE_WSTR**||O nome do cubo ao qual este membro pertence.|  
|**DIMENSION_UNIQUE_NAME**|**DBTYPE_WSTR**||O nome exclusivo da dimensão à qual este membro pertence.|  
|**HIERARCHY_UNIQUE_NAME**|**DBTYPE_WSTR**||O nome exclusivo da hierarquia à qual este membro pertence.|  
|**LEVEL_UNIQUE_NAME**|**DBTYPE_WSTR**||O nome exclusivo do nível ao qual este membro pertence.|  
|**LEVEL_NUMBER**|**DBTYPE_UI4**||A distância do membro para a raiz da hierarquia. O nível raiz é zero (0).|  
|**MEMBER_ORDINAL**|**DBTYPE_UI4**||(Preterido) Sempre retorna **0**.|  
|**MEMBER_NAME**|**DBTYPE_WSTR**||O nome do membro.|  
|**MEMBER_UNIQUE_NAME**|**DBTYPE_WSTR**||O nome exclusivo do membro.|  
|**MEMBER_TYPE**|**DBTYPE_I4**||O tipo do membro:<br /><br /> **MDMEMBER_TYPE_UNKNOWN** (**0**)<br /><br /> **MDMEMBER_TYPE_REGULAR** (**1**)<br /><br /> **MDMEMBER_TYPE_ALL** (**2**)<br /><br /> **MDMEMBER_TYPE_MEASURE** (**3**)<br /><br /> **MDMEMBER_TYPE_FORMULA** (**4**)<br /><br /> <br /><br /> Observe que <br />                    **MDMEMBER_TYPE_FORMULA**tem precedência sobre **MDMEMBER_TYPE_MEASURE**. Por exemplo, se houver um membro de fórmula (calculado) na dimensão medidas, ele é listado como **MDMEMBER_TYPE_FORMULA**.|  
|**MEMBER_GUID**|**DBTYPE_GUID**||O GUID do membro. **NULO** se não houver GUID.|  
|**MEMBER_CAPTION**|**DBTYPE_WSTR**||Um rótulo ou legenda associado ao membro. Usado principalmente para fins de exibição. Se não houver uma legenda, **MEMBER_NAME** é retornado.|  
|**CHILDREN_CARDINALITY**|**DBTYPE_UI4**||O número de filhos de um membro. Pode ser uma estimativa e, portanto, os consumidores não devem confiar nessa contagem como sendo exata. Os provedores devem retornar a melhor estimativa possível.|  
|**PARENT_LEVEL**|**DBTYPE_UI4**||A distância do pai do membro para o nível raiz da hierarquia. O nível raiz é zero (0).|  
|**PARENT_UNIQUE_NAME**|**DBTYPE_WSTR**||O nome exclusivo do pai do membro. **NULL** é retornado para qualquer membro no nível raiz.|  
|**PARENT_COUNT**|**DBTYPE_UI4**||O número de pais deste membro.|  
|**DESCRIPTION**|**DBTYPE_WSTR**||Essa coluna sempre retorna um **nulo** valor.<br /><br /> Esta coluna existe para compatibilidade com versões anteriores|  
|**EXPRESSÃO**|**DBTYPE_WSTR**||A expressão para cálculos, se o membro for do tipo **MDMEMBER_TYPE_FORMULA**.|  
|**MEMBER_KEY**|**DBTYPE_WSTR**||O valor da coluna de chave do membro. Retorna **nulo** se o membro tiver uma chave composta.|  
|**IS_PLACEHOLDERMEMBER**|**DBTYPE_BOOL**||Um booliano que indica se um membro é um membro de espaço reservado para uma posição vazia em uma hierarquia da dimensão.<br /><br /> Ele é válido somente se o **compatibilidade MDX** propriedade foi definida como 2.|  
|**IS_DATAMEMBER**|**DBTYPE_BOOL**||Um booliano que indica se o membro é ou não um membro de dados.<br /><br /> Retornará True se o membro for um membro de dados.|  
|**ESCOPO**|**DBTYPE_I4**||O escopo do membro. O membro pode ser um membro calculado da sessão ou um membro calculado global. Retorna a coluna **nulo** para membros não calculados. Esta coluna pode ter um dos seguintes valores:<br /><br /> MDMEMBER_SCOPE_GLOBAL=1<br /><br /> MDMEMBER_SCOPE_SESSION=2|  
|**Zero ou mais colunas adicionais**|**DBTYPE_UI2**||Nenhuma propriedade será retornada se os membros puderem ser retornados de vários níveis. Por exemplo, se o operador de árvore é **pai** e **SELF** para uma hierarquia não pai-filho, nenhuma propriedade de membro é retornada.<br /><br /> Isso se aplica a hierarquias desbalanceadas onde os operadores de árvore podem retornar membros de níveis diferentes (por exemplo, se o nível anterior contiver intervalos e se o pai de membros for solicitado). |  
  
 O conjunto de linhas é classificado em **CATALOG_NAME**, **SCHEMA_NAME**, **CUBE_NAME**, **DIMENSION_UNIQUE_NAME**, **HIERARCHY_ UNIQUE_NAME**, **LEVEL_UNIQUE_NAME**, **LEVEL_NUMBER**, **MEMBER_ORDINAL**.  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O **MDSCHEMA_MEMBERS** linhas pode ser restringido nas colunas listadas na tabela a seguir.  
  
|Nome da coluna|Indicador de tipo|Estado de restrição|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**CUBE_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**DIMENSION_UNIQUE_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**HIERARCHY_UNIQUE_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**LEVEL_UNIQUE_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**LEVEL_NUMBER**|**DBTYPE_UI4**|Opcional.|  
|**MEMBER_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**MEMBER_UNIQUE_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**MEMBER_CAPTION**|**DBTYPE_WSTR**|Opcional.|  
|**MEMBER_TYPE**|**DBTYPE_I4**|Opcional.|  
|**TREE_OP**|**DBTYPE_I4**|(Opcional) Só se aplica a um único membro:<br /><br /> **MDTREEOP_ANCESTORS** (**0x20**) retorna todos os ancestrais.<br /><br /> **MDTREEOP_CHILDREN** (**0x01**) retorna somente os filhos imediatos.<br /><br /> **MDTREEOP_SIBLINGS** (**0x02**) Retorna membros no mesmo nível.<br /><br /> **MDTREEOP_PARENT** (**0x04**) retorna somente o pai imediato.<br /><br /> **MDTREEOP_SELF** (**0x08**) retorna ele mesmo na lista de linhas retornadas.<br /><br /> **MDTREEOP_DESCENDANTS** (**0x10**) retorna todos os descendentes.|  
|**CUBE_SOURCE**|**DBTYPE_UI2**|(Opcional) A restrição padrão é um valor de 1. Um bitmap com um dos seguintes valores válidos:<br /><br /> 1 CUBO<br /><br /> 2 DIMENSÃO|  
  
## <a name="see-also"></a>Consulte também  
 [Conjuntos de linhas de esquema OLE DB para OLAP](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
