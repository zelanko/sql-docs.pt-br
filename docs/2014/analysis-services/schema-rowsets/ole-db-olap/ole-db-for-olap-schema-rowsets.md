---
title: OLE DB para OLAP Schema Rowsets | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- schema rowsets [Analysis Services], OLE DB for OLAP
- OLE DB for OLAP schema rowsets
- schema rowsets [OLE DB for OLAP]
- rowsets [Analysis Services], OLE DB for OLAP
ms.assetid: 5fad3ecc-407c-4148-862e-ea6119cc7480
caps.latest.revision: 31
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 406451b0e8e6edce92d69cde493888f70813f4de
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37306476"
---
# <a name="ole-db-for-olap-schema-rowsets"></a>Conjuntos de linhas de esquema OLE DB para OLAP
  O provedor do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XML for Analysis (XMLA) dá suporte aos conjuntos de linhas de esquema OLE DB para OLAP a seguir.  
  
> [!NOTE]  
>  Para verificar se um provedor de fonte de dados específico dá suporte a um conjunto de linhas, use o `DISCOVER_ENUMERATIONS` conjunto de linhas com o [Discover](../../xmla/xml-elements-methods-discover.md) método.  
  
 Você também pode encontrar informações detalhadas sobre esses conjuntos de linhas pesquisando o tópico "OLAP Schema Rowsets", na biblioteca MSDN em isso [site da Microsoft](http://go.microsoft.com/fwlink/?LinkId=15426).  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Linhas de esquema<sup>1</sup>|Description|  
|-------------------------------|-----------------|  
|[Conjunto de linhas DISCOVER_INSTANCES](discover-instances-rowset.md)|Descreve as instâncias no servidor.|  
|[Conjunto de linhas DISCOVER_KEYWORDS &#40;OLE DB para OLAP&#41;](discover-keywords-rowset-ole-db-for-olap.md)|Enumera uma lista de palavras reservadas pelo provedor.|  
|[Conjunto de linhas MDSCHEMA_ACTIONS](mdschema-actions-rowset.md)|Descreve as ações que podem estar disponíveis ao aplicativo cliente.|  
|[Conjunto de linhas MDSCHEMA_CUBES](mdschema-cubes-rowset.md)|Descreve a estrutura de cubos dentro de um banco de dados.|  
|[Conjunto de linhas MDSCHEMA_DIMENSIONS](mdschema-dimensions-rowset.md)|Descreve as dimensões compartilhadas e privadas dentro de um banco de dados.|  
|[Conjunto de linhas MDSCHEMA_FUNCTIONS](mdschema-functions-rowset.md)|Descreve as funções que estão disponíveis para aplicativos cliente conectados ao banco de dados.|  
|[Conjunto de linhas MDSCHEMA_HIERARCHIES](mdschema-hierarchies-rowset.md)|Descreve cada hierarquia encontrada em determinada dimensão.|  
|[Conjunto de linhas MDSCHEMA_INPUT_DATASOURCES](mdschema-input-datasources-rowset.md)|Descreve as fontes de dados definidas dentro do banco de dados.|  
|[Conjunto de linhas MDSCHEMA_KPIS](mdschema-kpis-rowset.md)|Descreve os KPIs (indicadores chave de desempenho) dentro de um banco de dados.|  
|[Conjunto de linhas MDSCHEMA_LEVELS](mdschema-levels-rowset.md)|Descreve cada nível dentro de uma hierarquia específica.|  
|[Conjunto de linhas MDSCHEMA_MEASUREGROUP_DIMENSIONS](mdschema-measuregroup-dimensions-rowset.md)|Enumera as dimensões de grupos de medidas.|  
|[Conjunto de linhas MDSCHEMA_MEASURESGROUPS](mdschema-measuregroups-rowset.md)|Descreve os grupos de medidas dentro de um banco de dados.|  
|[Conjunto de linhas MDSCHEMA_MEASURES](mdschema-measures-rowset.md)|Descreve cada medida dentro de um cubo.|  
|[Conjunto de linhas MDSCHEMA_MEMBERS](mdschema-members-rowset.md)|Descreve os membros dentro de um banco de dados.|  
|[Conjunto de linhas MDSCHEMA_PROPERTIES](mdschema-properties-rowset.md)|Descreve as propriedades de membros dentro de um banco de dados.|  
|[Conjunto de linhas MDSCHEMA_SETS](mdschema-sets-rowset.md)|Descreve qualquer conjunto definido atualmente em um banco de dados, incluindo conjuntos do escopo da sessão.|  
  
 <sup>1</sup> todas as linhas do esquema listadas aqui são suportadas pelo provedor de fonte de dados MSOLAP para o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] provedor XMLA.  
  
## <a name="see-also"></a>Consulte também  
 [Conjunto de linhas DISCOVER_ENUMERATORS](../xml/discover-enumerators-rowset.md)   
 [Conjuntos de linhas de esquema do Analysis Services](../../schema-rowsets/analysis-services-schema-rowsets.md)  
  
  
