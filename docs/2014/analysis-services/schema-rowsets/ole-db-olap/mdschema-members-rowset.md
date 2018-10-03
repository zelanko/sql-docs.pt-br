---
title: Conjunto de linhas MDSCHEMA_MEMBERS | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- MDSCHEMA_MEMBERS
topic_type:
- apiref
helpviewer_keywords:
- MDSCHEMA_MEMBERS rowset
ms.assetid: 0b1aada0-67f8-4ef6-81b2-0100b65e0c2f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: dbe7db640163f539ba15e8418177846564731148
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48133896"
---
# <a name="mdschemamembers-rowset"></a>Conjunto de linhas MDSCHEMA_MEMBERS
  Descreve os membros dentro de um banco de dados.  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O `MDSCHEMA_MEMBERS` linhas contém as colunas a seguir.  
  
|Nome da coluna|Indicador de tipo|Comprimento|Description|  
|-----------------|--------------------|------------|-----------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`||O nome do banco de dados ao qual este membro pertence.|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`||O nome do esquema ao qual este membro pertence.|  
|`CUBE_NAME`|`DBTYPE_WSTR`||O nome do cubo ao qual este membro pertence.|  
|`DIMENSION_UNIQUE_NAME`|`DBTYPE_WSTR`||O nome exclusivo da dimensão à qual este membro pertence.|  
|`HIERARCHY_UNIQUE_NAME`|`DBTYPE_WSTR`||O nome exclusivo da hierarquia à qual este membro pertence.|  
|`LEVEL_UNIQUE_NAME`|`DBTYPE_WSTR`||O nome exclusivo do nível ao qual este membro pertence.|  
|`LEVEL_NUMBER`|`DBTYPE_UI4`||A distância do membro para a raiz da hierarquia. O nível raiz é zero (0).|  
|`MEMBER_ORDINAL`|`DBTYPE_UI4`||(Substituído) Sempre retorna `0`.|  
|`MEMBER_NAME`|`DBTYPE_WSTR`||O nome do membro.|  
|`MEMBER_UNIQUE_NAME`|`DBTYPE_WSTR`||O nome exclusivo do membro.|  
|`MEMBER_TYPE`|`DBTYPE_I4`||O tipo do membro:<br /><br /> -   `MDMEMBER_TYPE_REGULAR` (`1`)<br />-   `MDMEMBER_TYPE_ALL` (`2`)<br />-   `MDMEMBER_TYPE_MEASURE` (`3`)<br />-   `MDMEMBER_TYPE_FORMULA` (`4`)<br />-   `MDMEMBER_TYPE_UNKNOWN` (`0`)<br />-   `MDMEMBER_TYPE_FORMULA` tem precedência sobre `MDMEMBER_TYPE_MEASURE`. Por exemplo, se houver um membro de fórmula (calculado) na dimensão Medidas, será listado como `MDMEMBER_TYPE_FORMULA`.|  
|`MEMBER_GUID`|`DBTYPE_GUID`||O GUID do membro. `NULL` se nenhum GUID existir.|  
|`MEMBER_CAPTION`|`DBTYPE_WSTR`||Um rótulo ou legenda associado ao membro. Usado principalmente para fins de exibição. Se não houver uma legenda, `MEMBER_NAME` será retornado.|  
|`CHILDREN_CARDINALITY`|`DBTYPE_UI4`||O número de filhos de um membro. Pode ser uma estimativa e, portanto, os consumidores não devem confiar nessa contagem como sendo exata. Os provedores devem retornar a melhor estimativa possível.|  
|`PARENT_LEVEL`|`DBTYPE_UI4`||A distância do pai do membro para o nível raiz da hierarquia. O nível raiz é zero (0).|  
|`PARENT_UNIQUE_NAME`|`DBTYPE_WSTR`||O nome exclusivo do pai do membro. `NULL` é retornado para qualquer membro no nível raiz.|  
|`PARENT_COUNT`|`DBTYPE_UI4`||O número de pais deste membro.|  
|`DESCRIPTION`|`DBTYPE_WSTR`||Essa coluna sempre retorna um valor `NULL`.<br /><br /> Esta coluna existe para compatibilidade com versões anteriores|  
|`EXPRESSION`|`DBTYPE_WSTR`||A expressão para cálculos, se o membro for de tipo `MDMEMBER_TYPE_FORMULA`.|  
|`MEMBER_KEY`|`DBTYPE_WSTR`||O valor da coluna de chave do membro. Retorna `NULL` se o membro tiver uma chave composta.|  
|`IS_PLACEHOLDERMEMBER`|`DBTYPE_BOOL`||Um booliano que indica se um membro é um membro de espaço reservado para uma posição vazia em uma hierarquia da dimensão.<br /><br /> Só será válido se a propriedade `MDX Compatibility` foi definida como 2.|  
|`IS_DATAMEMBER`|`DBTYPE_BOOL`||Um booliano que indica se o membro é ou não um membro de dados.<br /><br /> Retornará True se o membro for um membro de dados.|  
|`SCOPE`|`DBTYPE_I4`||O escopo do membro. O membro pode ser um membro calculado da sessão ou um membro calculado global. A coluna retorna `NULL` para membros não calculados.<br /><br /> Esta coluna pode ter um dos seguintes valores:<br /><br /> -MDMEMBER_SCOPE_GLOBAL = 1<br />-MDMEMBER_SCOPE_SESSION = 2|  
|`Zero or more additional columns`|`DBTYPE_UI2`||Nenhuma propriedade será retornada se os membros puderem ser retornados de vários níveis. Por exemplo, se o operador Árvore for `PARENT` e `SELF` para uma hierarquia que seja do tipo pai-filho, nenhuma propriedade do membro será retornada.<br /><br /> Isso se aplica a hierarquias desbalanceadas onde os operadores de árvore podem retornar membros de níveis diferentes (por exemplo, se o nível anterior contiver intervalos e se o pai de membros for solicitado). |  
  
 O conjunto de linhas é classificado em `CATALOG_NAME`, `SCHEMA_NAME`, `CUBE_NAME`, `DIMENSION_UNIQUE_NAME`, `HIERARCHY_UNIQUE_NAME`, `LEVEL_UNIQUE_NAME`, `LEVEL_NUMBER`, `MEMBER_ORDINAL`.  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O conjunto de linhas `MDSCHEMA_MEMBERS` pode ser restringido nas colunas listadas na tabela a seguir.  
  
|Nome da coluna|Indicador de tipo|Estado de restrição|  
|-----------------|--------------------|-----------------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`CUBE_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`DIMENSION_UNIQUE_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`HIERARCHY_UNIQUE_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`LEVEL_UNIQUE_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`LEVEL_NUMBER`|`DBTYPE_UI4`|Opcional.|  
|`MEMBER_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`MEMBER_UNIQUE_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`MEMBER_CAPTION`|`DBTYPE_WSTR`|Opcional.|  
|`MEMBER_TYPE`|`DBTYPE_I4`|Opcional.|  
|`TREE_OP`|`DBTYPE_I4`|(Opcional) Só se aplica a um único membro:<br /><br /> -   `MDTREEOP_ANCESTORS` (`0x20`) retorna todos os ancestrais.<br />-   `MDTREEOP_CHILDREN` (`0x01`) retorna somente os filhos imediatos.<br />-   `MDTREEOP_SIBLINGS` (`0x02`) retorna os membros no mesmo nível.<br />-   `MDTREEOP_PARENT` (`0x04`) retorna somente o pai imediato.<br />-   `MDTREEOP_SELF` (`0x08`) retorna ele próprio na lista de linhas retornadas.<br />-   `MDTREEOP_DESCENDANTS` (`0x10`) retorna todos os descendentes.|  
|`CUBE_SOURCE`|`DBTYPE_UI2`|(Opcional) Um bitmap com um dos seguintes valores válidos:<br /><br /> -CUBO DE 1<br />-DIMENSÃO DE 2<br /><br /> A restrição padrão tem valor 1.|  
  
## <a name="see-also"></a>Consulte também  
 [Conjuntos de linhas de esquema OLE DB para OLAP](ole-db-for-olap-schema-rowsets.md)  
  
  
