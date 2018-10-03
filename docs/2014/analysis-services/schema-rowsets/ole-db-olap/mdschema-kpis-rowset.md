---
title: Conjunto de linhas MDSCHEMA_KPIS | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- MDSCHEMA_KPIS
topic_type:
- apiref
helpviewer_keywords:
- MDSCHEMA_KPIS rowset
ms.assetid: 40fb5112-6a90-4455-82b3-8b6322490222
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 77f6dc3fd3f8e9c92fe1d840c9af646269e0effc
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48124456"
---
# <a name="mdschemakpis-rowset"></a>Conjunto de linhas MDSCHEMA_KPIS
  Descreve os KPIs (indicadores chave de desempenho) dentro de um banco de dados.  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O `MDSCHEMA_KPIS` linhas contém as colunas a seguir.  
  
|Nome da coluna|Indicador de tipo|Comprimento|Description|  
|-----------------|--------------------|------------|-----------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`||O banco de dados de origem.|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`||Sem suporte.|  
|`CUBE_NAME`|`DBTYPE_WSTR`||O cubo pai para o KPI.|  
|`MEASUREGROUP_NAME`|`DBTYPE_WSTR`||O grupo de medidas associado para o KPI.<br /><br /> Você pode usar esta coluna para determinar a dimensionalidade do KPI. Se "**\<nula >**", o KPI será dimensionado por todos os grupos de medidas.<br /><br /> O valor padrão é "**\<nula >**".|  
|`KPI_NAME`|`DBTYPE_WSTR`||O nome do KPI.|  
|`KPI_CAPTION`|`DBTYPE_WSTR`||Um rótulo ou uma legenda associada ao KPI. Usado principalmente para fins de exibição. Se não houver uma legenda, `KPI_NAME` será retornado.|  
|`KPI_DESCRIPTION`|`DBTYPE_WSTR`||Uma descrição legível do KPI.|  
|`KPI_DISPLAY_FOLDER`|`DBTYPE_WSTR`||Uma cadeia de caracteres que identifica o caminho da pasta de exibição que o aplicativo cliente usa para mostrar o membro. O separador de nível de pasta é definido pelo aplicativo cliente. Para as ferramentas e clientes fornecidos pelo [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], a barra invertida (\\) é o separador de nível. Para fornecer várias pastas de exibição, use um ponto e vírgula (;) para separar as pastas.|  
|`KPI_VALUE`|`DBTYPE_WSTR`||O nome exclusivo do membro na dimensão de medidas para o Valor do KPI.|  
|`KPI_GOAL`|`DBTYPE_WSTR`||O nome exclusivo do membro na dimensão de medidas para a Meta do KPI.<br /><br /> Retornará `NULL` se não houver uma Meta definida.|  
|`KPI_STATUS`|`DBTYPE_WSTR`||O nome exclusivo do membro na dimensão de medidas para o Status do KPI.<br /><br /> Retornará `NULL` se não houver um Status definido.|  
|`KPI_TREND`|`DBTYPE_WSTR`||O nome exclusivo do membro na dimensão de medidas para a Tendência do KPI.<br /><br /> Retornará `NULL` se não houver uma Tendência definida.|  
|`KPI_STATUS_GRAPHIC`|`DBTYPE_WSTR`||A representação gráfica padrão do KPI.|  
|`KPI_TREND_GRAPHIC`|`DBTYPE_WSTR`||A representação gráfica padrão do KPI.|  
|`KPI_WEIGHT`|`DBTYPE_WSTR`||O nome exclusivo do membro na dimensão de medidas para o Peso do KPI.|  
|`KPI_CURRENT_TIME_MEMBER`|`DBTYPE_WSTR`||O nome exclusivo do membro na dimensão de tempo que define o contexto temporal do KPI.<br /><br /> Retornará `NULL` se não houver um membro definido de Tempo.|  
|`KPI_PARENT_KPI_NAME`|`DBTYPE_WSTR`||O nome do KPI pai.|  
|`SCOPE`|`DBTYPE_I4`||O escopo do KPI. O KPI pode ser um KPI de sessão ou um KPI global.<br /><br /> Esta coluna pode ter um dos seguintes valores:<br /><br /> -MDKPI_SCOPE_GLOBAL = 1<br />-MDKPI_SCOPE_SESSION = 2|  
|`ANNOTATIONS`|`DBTYPE_WSTR`||(Opcional) Um conjunto de notas em formato XML.|  
  
 Este conjunto de linhas do esquema não é classificado.  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O conjunto de linhas `MDSCHEMA_KPIS` pode ser restringido nas colunas listadas na tabela a seguir.  
  
|Nome da coluna|Indicador de tipo|Estado de restrição|  
|-----------------|--------------------|-----------------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`CUBE_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`KPI_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`CUBE_SOURCE`|`DBTYPE_UI2`|(Opcional) Um bitmap com um dos seguintes valores válidos:<br /><br /> -   `1` CUBO<br />-   `2` DIMENSÃO<br /><br /> A restrição padrão é um valor `1`.|  
  
## <a name="see-also"></a>Consulte também  
 [Conjuntos de linhas de esquema OLE DB para OLAP](ole-db-for-olap-schema-rowsets.md)  
  
  
