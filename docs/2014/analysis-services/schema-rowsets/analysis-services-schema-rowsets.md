---
title: Conjuntos de linhas de esquema do Analysis Services | Microsoft Docs
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
topic_type:
- apiref
- apinav
helpviewer_keywords:
- SSAS, data access interfaces
- Analysis Services data access interfaces, schema rowsets
- data access interfaces [Analysis Services]
- XML for Analysis, schema rowsets
- rowsets [Analysis Services], retrieving schema rowsets
- retrieving schema rowsets
- XMLA, schema rowsets
- rowsets [Analysis Services]
- schema rowsets [Analysis Services], retrieving
ms.assetid: 820d4b59-d428-4616-b792-c848e5da407e
caps.latest.revision: 31
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d01770593787032d96ab869dd59cd40658eca4b0
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37153227"
---
# <a name="analysis-services-schema-rowsets"></a>Conjuntos de linhas de esquema do Analysis Services
  Conjuntos de linhas de esquema são tabelas predefinidas que contêm informações sobre objetos do Analysis Services e o estado do servidor, inclusive esquema de banco de dados, sessões ativas, conexões, comandos e trabalhos executados no servidor. Você pode consultar as tabelas de conjunto de linhas de esquema em uma janela de script XML/UM no SQL Server Management Studio, executar uma consulta de DMV em relação a um conjunto de linhas de esquema ou criar um aplicativo personalizado que incorpora informações de conjunto de linhas de esquema (por exemplo, um aplicativo de relatório que recupera a lista de dimensões disponíveis que podem ser usadas para criar um relatório).  
  
> [!NOTE]  
>  Se você estiver usando conjuntos de linhas de esquema no XML/A script, as informações retornadas na *resultado* parâmetro do [Discover](../xmla/xml-elements-methods-discover.md) método é estruturado de acordo com os layouts da coluna de conjunto de linhas descritos neste seção. O provedor do [!INCLUDE[msCoName](../../includes/msconame-md.md)] XML for Analysis (XMLA) dá suporte a conjuntos de linhas requeridos pela Especificação do XML for Analysis. O provedor do XMLA também dá suporte a alguns dos conjuntos de linhas de esquema padrão para os provedores de fonte de dados OLE DB, OLE DB para OLAP e OLE DB para Mineração de Dados. Os conjuntos de linhas suportados são descritos nos tópicos a seguir.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Conjunto de linhas de esquema do XML](xml/xml-for-analysis-schema-rowsets.md)|Descreve os conjuntos de linhas XMLA suportados pelo provedor XMLA.|  
|[Conjuntos de linhas do esquema OLE DB](ole-db/ole-db-schema-rowsets.md)|Descreve os conjuntos de linhas de esquema OLE DB suportados pelo provedor do XMLA.|  
|[Conjuntos de linhas de esquema OLE DB para OLAP](ole-db-olap/ole-db-for-olap-schema-rowsets.md)|Descreve os conjuntos de linhas de esquema OLE DB para OLAP suportados pelo provedor do XMLA.|  
|[Conjuntos de linhas de esquema de mineração de dados](data-mining/data-mining-schema-rowsets.md)|Descreve os conjuntos de linhas de esquema de mineração de dados suportados pelo provedor do XMLA.|  
  
## <a name="see-also"></a>Consulte também  
 [Acesso a dados modelo multidimensional &#40;Analysis Services - dados multidimensionais&#41;](../multidimensional-models/mdx/multidimensional-model-data-access-analysis-services-multidimensional-data.md)   
 [Usar exibições de gerenciamento dinâmico &#40;DMVs&#41; monitorar o Analysis Services](../instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)  
  
  
