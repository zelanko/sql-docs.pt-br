---
title: Recursos de pesquisa de texto completo no SQL Server 2014 preteridos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- deprecated features [full-text search]
- full-text search [SQL Server], deprecated features
- full-text queries [SQL Server], proximity
ms.assetid: ab0d799c-ba79-4459-837b-c4862730dafd
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 1a49d7db68fe32d9794e89db66020d7f90555508
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66011398"
---
# <a name="deprecated-full-text-search-features-in-sql-server-2014"></a>Recursos de pesquisa de texto completo obsoletos no SQL Server 2014
  Este tópico descreve os recursos de pesquisa de texto completo preteridos que ainda estão disponíveis no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Esses recursos estão programados para serem removidos em uma versão futura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Recursos preteridos não devem ser usados em aplicativos novos.  
  
 É possível monitorar o uso de recursos preteridos usando o contador de desempenho do Objeto e eventos de rastreamento do **SQL Server: Recursos Preteridos** . Para obter mais informações, confira o artigo [Usar objetos do SQL Server](../performance-monitor/use-sql-server-objects.md).  
  
## <a name="features-not-supported-in-the-next-version-of-sql-server"></a>Recursos sem suporte na próxima versão do SQL Server  
 Os recursos de pesquisa de texto completo a seguir não terão suporte na próxima versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Recurso substituído|Substituição|Nome do recurso|ID do Recurso|  
|------------------------|-----------------|------------------|----------------|  
|Propriedade FULLTEXTCATALOGPROPERTY: LogSize|Nenhum.|FULLTEXTCATALOGPROPERTY **('LogSize')**|211|  
|Propriedade FULLTEXTSERVICEPROPERTY:<br /><br /> ConnectTimeout<br /><br /> DataTimeout|Nenhum.|FULLTEXTSERVICEPROPERTY **('ConnectTimeout')**<br /><br /> FULLTEXTSERVICEPROPERTY **('DataTimeout'** )|210<br /><br /> 209|  
|sp_fulltext_catalog|CREATE FULL CATALOG<br /><br /> ALTER FULLTEXT CATALOG<br /><br /> DROP FULLTEXT CATALOG|sp_fulltext_catalog|84|  
|sp_fulltext_column<br /><br /> sp_fulltext_database<br /><br /> sp_fulltext_table|CREATE FULL INDEX<br /><br /> ALTER FULLTEXT INDEX<br /><br /> DROP FULLTEXT INDEX|sp_fulltext_column<br /><br /> sp_fulltext_database<br /><br /> sp_fulltext_table|86<br /><br /> 87<br /><br /> 85|  
|sp_help_fulltext_catalogs<br /><br /> sp_help_fulltext_catalog_components<br /><br /> sp_help_fulltext_catalogs_cursor<br /><br /> sp_help_fulltext_columns<br /><br /> sp_help_fulltext_columns_cursor<br /><br /> sp_help_fulltext_tables<br /><br /> sp_help_fulltext_tables_cursor|sys.fulltext_catalogs<br /><br /> sys.fulltext_index_columns<br /><br /> sys.fulltext_indexes|sp_help_fulltext_catalogs<br /><br /> sp_help_fulltext_catalog_components<br /><br /> sp_help_fulltext_catalogs_cursor<br /><br /> sp_help_fulltext_columns<br /><br /> sp_help_fulltext_columns_cursor<br /><br /> sp_help_fulltext_table<br /><br /> sp_help_fulltext_tables_cursor|88<br /><br /> 203<br /><br /> 90<br /><br /> 92<br /><br /> 93<br /><br /> 91<br /><br /> 89|  
|Os valores da ação sp_fulltext_service: clean_up, connect_timeout e data_timeout retornam zero|None|sp_fulltext_service @action=clean_up<br /><br /> sp_fulltext_service @action=connect_timeout<br /><br /> sp_fulltext_service @action=data_timeout|116<br /><br /> 117<br /><br /> 118|  
|Colunas de sys.dm_fts_active_catalogs:<br /><br /> is_paused<br /><br /> previous_status<br /><br /> previous_status_description<br /><br /> row_count_in_thousands<br /><br /> status<br /><br /> status_description<br /><br /> worker_count|Nenhum.|dm_fts_active_catalogs.is_paused<br /><br /> dm_fts_active_catalogs.previous_status<br /><br /> dm_fts_active_catalogs.previous_status_description<br /><br /> dm_fts_active_catalogs.row_count_in_thousands<br /><br /> dm_fts_active_catalogs.status<br /><br /> dm_fts_active_catalogs.status_description<br /><br /> dm_fts_active_catalogs.worker_count|218<br /><br /> 221<br /><br /> 222<br /><br /> 224<br /><br /> 219<br /><br /> 220<br /><br /> 223|  
|Coluna de sys.dm_fts_memory_buffers:<br /><br /> row_count|Nenhum.|dm_fts_memory_buffers.row_count|225|  
|Colunas de sys.fulltext_catalogs:<br /><br /> path<br /><br /> data_space_id<br /><br /> Colunas de file_id|Nenhum.|fulltext_catalogs.path<br /><br /> fulltext_catalogs.data_space_id<br /><br /> fulltext_catalogs.file_id|215<br /><br /> 216<br /><br /> 217|  
  
## <a name="features-not-supported-in-a-future-version-of-sql-server"></a>Recursos sem suporte em uma versão futura do SQL Server  
 Os recursos de pesquisa de texto completo a seguir terão suporte na próxima versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], mas serão removidos em uma versão posterior. A versão específica do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não foi determinada.  
  
 O valor **Nome do recurso** aparece em eventos de rastreamento como o ObjectName, e em contadores de desempenho e sys.dm_os_performance_counters como o nome de instância. O valor **ID do Recurso** aparece em eventos de rastreamento como o ObjectId.  
  
|Recurso substituído|Substituição|Nome do recurso|ID do Recurso|  
|------------------------|-----------------|------------------|----------------|  
|Operador NEAR genérico CONTAINS e CONTAINSTABLE:<br /><br /> {<simple_term> &#124; <prefix_term>}<br /><br /> {<br /><br /> { { NEAR &#124; ~ }    {<simple_term> &#124; <prefix_term>} } [...*n*]<br /><br /> }|O operador NEAR personalizado:<br /><br /> NEAR(<br /><br /> {   {<simple_term> &#124; <prefix_term>} [ ,...*n* ]<br /><br /> &#124; ( {<simple_term> &#124; <prefix_term>} [,...*n*] )<br /><br /> [,\<distance> [,\<order>] ]<br /><br /> }<br /><br /> )<br /><br /> \<distance> ::= {*integer* &#124; **MAX**}<br /><br /> \<order> ::= {TRUE &#124; **FALSE**}|FULLTEXT_OLD_NEAR_SYNTAX|247|  
|Opção CREATE FULLTEXT CATALOG:<br /><br /> IN PATH '*rootpath*'<br /><br /> ON FILEGROUP *filegroup*|Nenhum.|CREATE FULLTEXT CATLOG IN PATH<br /><br /> Nenhum.*|237<br /><br /> Nenhum.<sup>*</sup>|  
|Propriedade DATABASEPROPERTYEX: IsFullTextEnabled|Nenhum.|DATABASEPROPERTYEX **('IsFullTextEnabled')**|202|  
|Opção sp_detach_db:<br /><br /> [ @keepfulltextindexfile = ] '*KeepFulltextIndexFile*'|Nenhum.|sp_detach_db @keepfulltextindexfile|226|  
|Os valores da ação sp_fulltext_service: resource_usage não têm nenhuma função.|None|sp_fulltext_service @action=resource_usage|200|  
  
 \*O objeto **SQL Server:Deprecated Features** não monitora ocorrências de CREATE FULLTEXT CATLOG ON FILEGROUP *filegroup*.  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server, objeto recursos preteridos](../performance-monitor/sql-server-deprecated-features-object.md)   
 [Alterações significativas para pesquisa de texto completo](../../database-engine/breaking-changes-to-full-text-search.md)   
 [Recursos do Mecanismo de Banco de Dados preteridos no SQL Server 2014](../../database-engine/deprecated-database-engine-features-in-sql-server-2016.md)  
  
  
