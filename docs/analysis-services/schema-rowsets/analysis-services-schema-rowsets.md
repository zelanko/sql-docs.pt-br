---
title: Conjuntos de linhas do esquema do Analysis Services | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ea3d947e8cfbea4b183f4416ebabf6bb0ebf7b61
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34027796"
---
# <a name="analysis-services-schema-rowsets"></a>Conjuntos de linhas de esquema do Analysis Services
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Conjuntos de linhas de esquema são tabelas predefinidas que contêm informações sobre objetos do Analysis Services e o estado do servidor, inclusive esquema de banco de dados, sessões ativas, conexões, comandos e trabalhos executados no servidor. Você pode consultar as tabelas de conjunto de linhas de esquema em uma janela de script XML/UM no SQL Server Management Studio, executar uma consulta de DMV em relação a um conjunto de linhas de esquema ou criar um aplicativo personalizado que incorpora informações de conjunto de linhas de esquema (por exemplo, um aplicativo de relatório que recupera a lista de dimensões disponíveis que podem ser usadas para criar um relatório).  
  
> [!NOTE]  
>  Se você estiver usando conjuntos de linhas de esquema no XML/um script, as informações retornadas no *resultados* parâmetro o [Discover](../../analysis-services/xmla/xml-elements-methods-discover.md) método é estruturado de acordo com os layouts de coluna do conjunto de linhas descritos nesta seção. O provedor do [!INCLUDE[msCoName](../../includes/msconame-md.md)] XML for Analysis (XMLA) dá suporte a conjuntos de linhas requeridos pela Especificação do XML for Analysis. O provedor do XMLA também dá suporte a alguns dos conjuntos de linhas de esquema padrão para os provedores de fonte de dados OLE DB, OLE DB para OLAP e OLE DB para Mineração de Dados. Os conjuntos de linhas suportados são descritos nos tópicos a seguir.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Description|  
|-----------|-----------------|  
|[XML for Analysis conjuntos de linhas de esquema](../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)|Descreve os conjuntos de linhas XMLA suportados pelo provedor XMLA.|  
|[Conjuntos de linhas do esquema OLE DB](../../analysis-services/schema-rowsets/ole-db/ole-db-schema-rowsets.md)|Descreve os conjuntos de linhas de esquema OLE DB suportados pelo provedor do XMLA.|  
|[OLE DB para OLAP Schema Rowsets](../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)|Descreve os conjuntos de linhas de esquema OLE DB para OLAP suportados pelo provedor do XMLA.|  
|[Linhas do esquema de mineração de dados](../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)|Descreve os conjuntos de linhas de esquema de mineração de dados suportados pelo provedor do XMLA.|  
  
## <a name="see-also"></a>Consulte também  
 [Acesso a dados modelo multidimensional & #40; Analysis Services - dados multidimensionais & #41;](../../analysis-services/multidimensional-models/mdx/multidimensional-model-data-access-analysis-services-multidimensional-data.md)   
 [Usar dinâmico exibições de gerenciamento & #40; DMVs & #41; para monitorar o Analysis Services](../../analysis-services/instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)  
  
  
