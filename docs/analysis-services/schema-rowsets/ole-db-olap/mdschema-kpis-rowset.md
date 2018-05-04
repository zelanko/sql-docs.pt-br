---
title: Conjunto de linhas MDSCHEMA_KPIS | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- MDSCHEMA_KPIS
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- MDSCHEMA_KPIS rowset
ms.assetid: 40fb5112-6a90-4455-82b3-8b6322490222
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 68c927acad41794a61892d638fe3423dacb3948d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="mdschemakpis-rowset"></a>Conjunto de linhas MDSCHEMA_KPIS
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Descreve os KPIs (indicadores chave de desempenho) dentro de um banco de dados.  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O **MDSCHEMA_KPIS** linhas contém as seguintes colunas.  
  
|Nome da coluna|Indicador de tipo|Description|  
|-----------------|--------------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|O banco de dados de origem.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|Sem suporte.|  
|**CUBE_NAME**|**DBTYPE_WSTR**|O cubo pai para o KPI.|  
|**MEASUREGROUP_NAME**|**DBTYPE_WSTR**|O grupo de medidas associado para o KPI.<br /><br /> Você pode usar esta coluna para determinar a dimensionalidade do KPI. Se "**\<nulo >**", o KPI será dimensionado por todos os grupos de medidas.<br /><br /> O valor padrão é "**\<nulo >**".|  
|**KPI_NAME**|**DBTYPE_WSTR**|O nome do KPI.|  
|**KPI_CAPTION**|**DBTYPE_WSTR**|Um rótulo ou uma legenda associada ao KPI. Usado principalmente para fins de exibição. Se não houver uma legenda, **KPI_NAME** é retornado.|  
|**KPI_DESCRIPTION**|**DBTYPE_WSTR**|Uma descrição legível do KPI.|  
|**KPI_DISPLAY_FOLDER**|**DBTYPE_WSTR**|Uma cadeia de caracteres que identifica o caminho da pasta de exibição que o aplicativo cliente usa para mostrar o membro. O separador de nível de pasta é definido pelo aplicativo cliente. Para ferramentas e clientes fornecidos pelo [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], a barra invertida (\\) é o separador de nível. Para fornecer várias pastas de exibição, use um ponto e vírgula (;) para separar as pastas.|  
|**KPI_VALUE**|**DBTYPE_WSTR**|O nome exclusivo do membro na dimensão de medidas para o Valor do KPI.|  
|**KPI_GOAL**|**DBTYPE_WSTR**|O nome exclusivo do membro na dimensão de medidas para a Meta do KPI.<br /><br /> Retorna **nulo** se não houver uma meta definida.|  
|**KPI_STATUS**|**DBTYPE_WSTR**|O nome exclusivo do membro na dimensão de medidas para o Status do KPI.<br /><br /> Retorna **nulo** se não há nenhum Status definido.|  
|**KPI_TREND**|**DBTYPE_WSTR**|O nome exclusivo do membro na dimensão de medidas para a Tendência do KPI.<br /><br /> Retorna **nulo** se há uma tendência definida.|  
|**KPI_STATUS_GRAPHIC**|**DBTYPE_WSTR**|A representação gráfica padrão do KPI.|  
|**KPI_TREND_GRAPHIC**|**DBTYPE_WSTR**|A representação gráfica padrão do KPI.|  
|**KPI_WEIGHT**|**DBTYPE_WSTR**|O nome exclusivo do membro na dimensão de medidas para o Peso do KPI.|  
|**KPI_CURRENT_TIME_MEMBER**|**DBTYPE_WSTR**|O nome exclusivo do membro na dimensão de tempo que define o contexto temporal do KPI.<br /><br /> Retorna **nulo** se não houver nenhum membro de tempo definido.|  
|**KPI_PARENT_KPI_NAME**|**DBTYPE_WSTR**|O nome do KPI pai.|  
|**ESCOPO**|**DBTYPE_I4**|O escopo do KPI. O KPI pode ser um KPI de sessão ou um KPI global.<br /><br /> Esta coluna pode ter um dos seguintes valores:<br /><br /> MDKPI_SCOPE_GLOBAL=1<br /><br /> MDKPI_SCOPE_SESSION=2|  
|**ANOTAÇÕES**|**DBTYPE_WSTR**|(Opcional) Um conjunto de notas em formato XML.|  
  
 Este conjunto de linhas do esquema não é classificado.  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O **MDSCHEMA_KPIS** linhas pode ser restringido nas colunas listadas na tabela a seguir.  
  
|Nome da coluna|Indicador de tipo|Estado de restrição|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**CUBE_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**KPI_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**CUBE_SOURCE**|**DBTYPE_UI2**|(Opcional) A restrição padrão é um valor de **1**. Um bitmap com um dos seguintes valores válidos:<br /><br /> **1** CUBO<br /><br /> **2** DIMENSÃO|  
  
## <a name="see-also"></a>Consulte também  
 [OLE DB para OLAP Schema Rowsets](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
