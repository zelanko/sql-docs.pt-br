---
title: OLE DB para OLAP Schema Rowsets | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- schema rowsets [Analysis Services], OLE DB for OLAP
- OLE DB for OLAP schema rowsets
- schema rowsets [OLE DB for OLAP]
- rowsets [Analysis Services], OLE DB for OLAP
ms.assetid: 5fad3ecc-407c-4148-862e-ea6119cc7480
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 655e40afe2808b5f26216923d54e474054170a54
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="ole-db-for-olap-schema-rowsets"></a>Conjuntos de linhas de esquema OLE DB para OLAP
  O provedor do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XML for Analysis (XMLA) dá suporte aos conjuntos de linhas de esquema OLE DB para OLAP a seguir.  
  
> [!NOTE]  
>  Para verificar se um provedor de fonte de dados específico oferece suporte a um conjunto de linhas, use o **DISCOVER_ENUMERATIONS** conjunto de linhas com o [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) método.  
  
 Você também pode encontrar informações detalhadas sobre esses conjuntos de linhas pesquisando o tópico "OLAP Schema Rowsets" na biblioteca MSDN em isso [site da Microsoft](http://go.microsoft.com/fwlink/?LinkId=15426).  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Conjunto de linhas de esquema<sup>1</sup>|Description|  
|-------------------------------|-----------------|  
|[Conjunto de linhas DISCOVER_INSTANCES](../../../analysis-services/schema-rowsets/ole-db-olap/discover-instances-rowset.md)|Descreve as instâncias no servidor.|  
|[Conjunto de linhas DISCOVER_KEYWORDS &#40; OLE DB para OLAP &#41;](../../../analysis-services/schema-rowsets/ole-db-olap/discover-keywords-rowset-ole-db-for-olap.md)|Enumera uma lista de palavras reservadas pelo provedor.|  
|[Conjunto de linhas MDSCHEMA_ACTIONS](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-actions-rowset.md)|Descreve as ações que podem estar disponíveis ao aplicativo cliente.|  
|[Conjunto de linhas MDSCHEMA_CUBES](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-cubes-rowset.md)|Descreve a estrutura de cubos dentro de um banco de dados.|  
|[Conjunto de linhas MDSCHEMA_DIMENSIONS](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-dimensions-rowset.md)|Descreve as dimensões compartilhadas e privadas dentro de um banco de dados.|  
|[Conjunto de linhas MDSCHEMA_FUNCTIONS](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-functions-rowset.md)|Descreve as funções que estão disponíveis para aplicativos cliente conectados ao banco de dados.|  
|[Conjunto de linhas MDSCHEMA_HIERARCHIES](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-hierarchies-rowset.md)|Descreve cada hierarquia encontrada em determinada dimensão.|  
|[Conjunto de linhas MDSCHEMA_INPUT_DATASOURCES](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-input-datasources-rowset.md)|Descreve as fontes de dados definidas dentro do banco de dados.|  
|[Conjunto de linhas MDSCHEMA_KPIS](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-kpis-rowset.md)|Descreve os KPIs (indicadores chave de desempenho) dentro de um banco de dados.|  
|[Conjunto de linhas MDSCHEMA_LEVELS](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-levels-rowset.md)|Descreve cada nível dentro de uma hierarquia específica.|  
|[Conjunto de linhas MDSCHEMA_MEASUREGROUP_DIMENSIONS](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-measuregroup-dimensions-rowset.md)|Enumera as dimensões de grupos de medidas.|  
|[Conjunto de linhas mdschema_measuresgroups](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-measuregroups-rowset.md)|Descreve os grupos de medidas dentro de um banco de dados.|  
|[Conjunto de linhas MDSCHEMA_MEASURES](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-measures-rowset.md)|Descreve cada medida dentro de um cubo.|  
|[Conjunto de linhas MDSCHEMA_MEMBERS](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-members-rowset.md)|Descreve os membros dentro de um banco de dados.|  
|[Conjunto de linhas MDSCHEMA_PROPERTIES](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-properties-rowset.md)|Descreve as propriedades de membros dentro de um banco de dados.|  
|[Conjunto de linhas MDSCHEMA_SETS](../../../analysis-services/schema-rowsets/ole-db-olap/mdschema-sets-rowset.md)|Descreve qualquer conjunto definido atualmente em um banco de dados, incluindo conjuntos do escopo da sessão.|  
  
 <sup>1</sup> todas as linhas do esquema listadas aqui são suportadas pelo provedor de fonte de dados MSOLAP para o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] provedor XMLA.  
  
## <a name="see-also"></a>Consulte também  
 [Conjunto de linhas DISCOVER_ENUMERATORS](../../../analysis-services/schema-rowsets/xml/discover-enumerators-rowset.md)   
 [Conjuntos de linhas do esquema do Analysis Services](../../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)  
  
  

