---
title: XML for Analysis conjuntos de linhas de esquema | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
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
- rowsets [Analysis Services], XML for Analysis
- XML for Analysis, schema rowsets
- schema rowsets [Analysis Services], XML for Analysis
- schema rowsets [XML for Analysis]
ms.assetid: 36e3ecfd-fcc3-415a-9c43-f59921d2468a
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 391f3ab14aef3680b9590e73c5bc94cc2e13b3a4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36013443"
---
# <a name="xml-for-analysis-schema-rowsets"></a>XML for Analysis Schema Rowsets
  O provedor do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XML for Analysis (XMLA) inclui conjuntos de linhas de esquema que retornam metadados sobre estado de servidor, atividade e objetos. Recuperar metadados será necessário se você estiver desenvolvendo um aplicativo cliente que se conecta a um modelo do Analysis Services cujas características e estrutura sejam variáveis.  
  
 Os conjuntos de linhas de esquema também proporcionam uma perspectiva de processos internos e operações que podem lhe ajudar a monitorar o servidor e solucionar problemas. Para oferecer melhor suporte a tarefas administrativas ad hoc, você pode executar uma consulta DMV (Exibição de Gerenciamento Dinâmico) na maioria dos conjuntos de linhas de esquema. As consultas DMV retornam resultados em um formato tabular legível que você pode exibir no [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)].  
  
 A tabela a seguir lista e descreve cada conjunto de linhas de esquema XMLA e identifica se ele retorna informações específicas para modelos de dados tabulares.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Rowset<sup>1</sup>|Description|  
|------------------------|-----------------|  
|[Conjunto de linhas DISCOVER_CALC_DEPENDENCY](discover-calc-dependency-rowset.md)|Retorna informações sobre dependências entre tabelas, colunas, medidas e fórmulas de coluna calculadas.<br /><br /> Aplica-se a modelos tabulares implantados em uma instância do Analysis Services e a modelos do PowerPivot em pastas de trabalho do Excel executados em um ambiente do SharePoint.|  
|[Conjunto de linhas DISCOVER_CONNECTIONS](discover-connections-rowset.md)|Oferece uso de recursos e de informações de atividade sobre as conexões atualmente abertas no servidor.|  
|[Conjunto de linhas DISCOVER_COMMAND_OBJECTS](discover-command-objects-rowset.md)|Oferece uso de recursos e informações de atividade sobre os objetos em uso pelo comando referenciado.|  
|[Conjunto de linhas DISCOVER_COMMANDS](discover-commands-rowset.md)|Oferece uso de recursos e informações de atividade sobre os comandos em execução ou os últimos comandos executados nas conexões abertas no servidor|  
|[Conjunto de linhas DISCOVER_CSDL_METADATA](discover-csdl-metadata-rowset.md)|Retorna uma definição XML de uma fonte de dados para um cliente que pode consumir um modelo tabular ou do PowerPivot e apresentar os dados de origem como parte de um relatório.<br /><br /> Aplica-se a modelos tabulares implantados em uma instância do Analysis Services e a modelos do PowerPivot em pastas de trabalho do Excel executados em um ambiente do SharePoint.|  
|[Conjunto de linhas DISCOVER_DATASOURCES](discover-datasources-rowset.md)|Retorna uma lista das fontes de dados do provedor do XMLA que estão disponíveis no servidor ou no serviço Web.|  
|[Conjunto de linhas DISCOVER_DB_CONNECTIONS](discover-db-connections-rowset.md)|Oferece uso de recursos e de informações de atividade sobre as conexões abertas no momento do servidor para um banco de dados.|  
|[Conjunto de linhas DISCOVER_DIMENSION_STAT](discover-dimension-stat-rowset.md)|Retorna as estatísticas sobre a dimensão especificada.|  
|[Conjunto de linhas DISCOVER_ENUMERATORS](discover-enumerators-rowset.md)|Retorna uma lista de nomes, tipos de dados e valores de enumeração dos enumeradores que recebem suporte do provedor do XMLA para uma fonte de dados específica.|  
|[Conjunto de linhas DISCOVER_JOBS](discover-jobs-rowset.md)|Oferece informações sobre os trabalhos ativos em execução no servidor.|  
|[Conjunto de linhas DISCOVER_KEYWORDS &#40;XMLA&#41;](discover-keywords-rowset-xmla.md)|Retorna informações sobre palavras-chave reservadas pelo provedor do XMLA.|  
|[Conjunto de linhas DISCOVER_LITERALS](discover-literals-rowset.md)|Retorna informações sobre literais, incluindo tipos de dados e valores, com suporte do provedor do XMLA.|  
|[Conjunto de linhas DISCOVER_LOCATIONS](discover-locations-rowset.md)|Retorna informações sobre o conteúdo de um arquivo de backup.|  
|[Conjunto de linhas DISCOVER_LOCKS](discover-locks-rowset.md)|Oferece informações sobre os bloqueios atuais no servidor.|  
|[Conjunto de linhas DISCOVER_MEMORYGRANT](discover-memorygrant-rowset.md)|Retorna uma lista de concessões de cota de memória interna que são usadas por trabalhos atualmente em execução no servidor.|  
|[Conjunto de linhas DISCOVER_MEMORYUSAGE](discover-memoryusage-rowset.md)|Retorna as estatísticas de uso da memória de vários objetos alocados pelo servidor.|  
|[Conjunto de linhas DISCOVER_OBJECT_ACTIVITY](discover-object-activity-rowset.md)|Oferece uso de recursos por objeto desde o início do serviço.|  
|[Conjunto de linhas DISCOVER_OBJECT_MEMORY_USAGE](discover-object-memory-usage-rowset.md)|Oferece informações sobre recursos de memória usados por objetos.|  
|[Conjunto de linhas DISCOVER_PARTITION_DIMENSION_STAT](discover-partition-dimension-stat-rowset.md)|Retorna estatísticas sobre a dimensão associada a uma partição.|  
|[Conjunto de linhas DISCOVER_PARTITION_STAT](discover-partition-stat-rowset.md)|Retorna estatísticas sobre agregações em uma partição específica.|  
|[Conjunto de linhas DISCOVER_PERFORMANCE_COUNTERS](discover-performance-counters-rowset.md)|Retorna o valor de um ou mais contadores de desempenho especificados.|  
|[Conjunto de linhas DISCOVER_PROPERTIES](discover-properties-rowset.md)|Retorna uma lista de informações e valores sobre o padrão e propriedades específicas do provedor que recebem suporte do provedor do XMLA para a fonte de dados especificada.|  
|[Conjunto de linhas DISCOVER_SCHEMA_ROWSETS](discover-schema-rowsets-rowset.md)|Retorna os nomes, as restrições, a descrição e outras informações para todos os valores de enumeração e quaisquer valores adicionais de enumeração específica de provedor que recebem suporte do provedor do XMLA.|  
|[Conjunto de linhas DISCOVER_SESSIONS](discover-sessions-rowset.md)|Oferece uso de recursos e de informações de atividade sobre as sessões atualmente abertas no servidor.|  
|[Conjunto de linhas DISCOVER_STORAGE_TABLE_COLUMN_SEGMENTS](discover-storage-table-column-segments-rowset.md)|Fornece informações em nível de coluna e segmento sobre tabelas de armazenamento usadas por um banco de dados tabular ou do PowerPivot.<br /><br /> Aplica-se a modelos tabulares implantados em uma instância do Analysis Services e a modelos do PowerPivot em pastas de trabalho do Excel executados em um ambiente do SharePoint.|  
|[Conjunto de linhas DISCOVER_STORAGE_TABLE_COLUMNS](discover-storage-table-columns-rowset.md)|Permite que cliente determine a atribuição de colunas para tabelas de armazenamento usadas por um banco de dados tabular ou do PowerPivot.<br /><br /> Aplica-se a modelos tabulares implantados em uma instância do Analysis Services e a modelos do PowerPivot em pastas de trabalho do Excel executados em um ambiente do SharePoint.|  
|[Conjunto de linhas DISCOVER_STORAGE_TABLES](discover-storage-tables-rowset.md)|Retorna informações sobre as tabelas usadas em um modelo.<br /><br /> Aplica-se a modelos tabulares implantados em uma instância do Analysis Services e a modelos do PowerPivot em pastas de trabalho do Excel executados em um ambiente do SharePoint.|  
|[Conjunto de linhas DISCOVER_TRACE_COLUMNS](discover-trace-columns-rowset.md)|Descreve as colunas de rastreamento fornecidas pelo provedor de rastreamento.|  
|[Conjunto de linhas DISCOVER_TRACE_DEFINITION_PROVIDERINFO](discover-trace-definition-providerinfo-rowset.md)|Retorna informações básicas sobre o provedor de rastreamento, como seu nome e descrição.|  
|[Conjunto de linhas DISCOVER_TRACE_EVENT_CATEGORIES](discover-trace-event-categories-rowset.md)|Descreve as categorias de evento fornecidas pelo provedor de rastreamento.|  
|[Conjunto de linhas DISCOVER_TRACES](discover-traces-rowset.md)|Retorna informações sobre rastreamentos executados em um servidor.|  
|[Conjunto de linhas DISCOVER_TRANSACTIONS](discover-transactions-rowset.md)|Retorna o conjunto atual de transações pendentes no sistema.|  
|[Conjunto de linhas DISCOVER_XML_METADATA](discover-xml-metadata-rowset.md)|Retorna um documento XML que descreve um objeto solicitado.|  
  
 <sup>1</sup> todas as linhas do esquema listadas aqui são suportadas pelo provedor de fonte de dados MSOLAP para o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] provedor XMLA.  
  
## <a name="see-also"></a>Consulte também  
 [Desenvolvendo com XMLA no Analysis Services](../../multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)   
 [Usar exibições de gerenciamento dinâmico &#40;DMVs&#41; monitorar o Analysis Services](../../instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)   
 [Recuperando metadados de uma fonte de dados analíticos](../../multidimensional-models-adomd-net-client/retrieving-metadata-from-an-analytical-data-source.md)  
  
  