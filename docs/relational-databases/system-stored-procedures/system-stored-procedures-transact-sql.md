---
title: Procedimentos armazenados do sistema (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/21/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sql13.TSQLSysNoExpandPortal.f1
- sql13.TSQLSysNoExpandPortal.f1_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- stored procedures [SQL Server]
- APIs [SQL Server]
- stored procedures [SQL Server], categories
- system stored procedures [SQL Server], categories
- system stored procedures [SQL Server]
ms.assetid: a5c4d5b8-5a24-4a2d-99b4-d003b546ee3a
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5791ad4e14525c0f72f21c300c0191e67e24ee12
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86007885"
---
# <a name="system-stored-procedures-transact-sql"></a>Procedimentos armazenados do sistema (Transact-SQL)
[!INCLUDE [sqlserver2016-asdb-asdbmi-asa](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa.md)]

  No [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], muitas atividades administrativas e informativas podem ser executadas com os procedimentos armazenados do sistema. Os procedimentos armazenados do sistema são agrupados nas categorias mostradas na tabela a seguir.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Categoria|Descrição|  
|--------------|-----------------|  
|[Procedimentos armazenados de replicação geográfica ativa](https://msdn.microsoft.com/library/81658ee4-4422-4d73-bf7a-86a07422cb0d)|Usado para gerenciar o gerenciamento de configurações de replicação geográfica ativa no banco de dados SQL do Azure|  
|[Procedimentos armazenados do catálogo](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)|Usados para implementar funções do dicionário de dados ODBC e isolar aplicativos ODBC de alterações feitas nas tabelas subjacentes do sistema.|  
|[Procedimentos armazenados de captura de alteração de dados](../../relational-databases/system-stored-procedures/change-data-capture-stored-procedures-transact-sql.md)|Usados para habilitar, desabilitar ou gerar relatórios de objetos de captura de dados de alterações.|  
|[Procedimentos armazenados de cursor](../../relational-databases/system-stored-procedures/cursor-stored-procedures-transact-sql.md)|Usados para implementar a funcionalidade variável do cursor.|  
|[Procedimentos armazenados de coletor de dados](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)|Usados para trabalhar com coletor de dados e os seguintes componentes: conjuntos, itens e tipos de coleta.|  
|[Procedimentos armazenados do Mecanismo de Banco de Dados](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)|Usados para manutenção geral do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].|  
|[Database Mail procedimentos armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)|Usados para executar operações de email em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Procedimentos armazenados do plano de manutenção de banco de dados](../../relational-databases/system-stored-procedures/database-maintenance-plan-stored-procedures-transact-sql.md)|Usados para configurar as tarefas de manutenção principais necessárias para gerenciar o desempenho do banco de dados.|  
|[Procedimentos armazenados de consultas distribuídas](../../relational-databases/system-stored-procedures/distributed-queries-stored-procedures-transact-sql.md)|Usados para implementar e gerenciar consultas distribuídas.|  
|[Procedimentos armazenados de FileStream e Filetable &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/54beca08-c012-4ebd-aa68-d8a10d221b64)|Usados para configurar e gerenciar os recursos FILESTREAM e FileTable.|  
|[Procedimentos armazenados de regras de firewall &#40;banco de dados SQL do Azure&#41;](../../relational-databases/system-stored-procedures/firewall-rules-stored-procedures-azure-sql-database.md)|Usado para configurar o Firewall do banco de dados SQL do Azure.|  
|[Procedimentos armazenados de pesquisa de texto completo](../../relational-databases/system-stored-procedures/full-text-search-and-semantic-search-stored-procedures-transact-sql.md)|Usados para implementar e consultar índices de texto completo.|  
|[Procedimentos armazenados estendidos gerais](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)|Usados para disponibilizar uma interface a partir de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para programas externos para várias atividades de manutenção.|  
|[Procedimentos armazenados de envio de logs](../../relational-databases/system-stored-procedures/log-shipping-stored-procedures-transact-sql.md)|Usados para configurar, modificar e monitorar configurações de envio de logs.|  
|[Procedimentos armazenados do data warehouse de gerenciamento &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/management-data-warehouse-stored-procedures-transact-sql.md)|Usado para configurar o data warehouse de gerenciamento.|  
|[Procedimentos armazenados de automação OLE](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)|Usados para ativar objetos padrão de automação para uso em um lote [!INCLUDE[tsql](../../includes/tsql-md.md)] padrão.|  
|[Procedimentos armazenados de Gerenciamento Baseados em Política](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)|Usado para Gerenciamento Baseado em Políticas.|  
|[Procedimentos armazenados do PolyBase](https://msdn.microsoft.com/library/a522b303-bd1b-410b-92d1-29c950a15ede)|Adicionar ou remover um computador de um grupo de escala horizontal do polybase.|  
|[Procedimentos Armazenados do Repositório de Consultas &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)|Usado para ajustar o desempenho.|  
|[Procedimentos Armazenados de Replicação](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)|Usados para gerenciar a replicação.|  
|[Procedimentos armazenados de segurança](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)|Usados para gerenciar a segurança.|  
|[Procedimentos armazenados de backup de instantâneo](https://msdn.microsoft.com/library/c278db87-5770-4037-a1e6-b9853a943339)|Usado para excluir o backup de FILE_SNAPSHOT junto com todos os seus instantâneos ou para excluir um instantâneo de arquivo de backup individual.|  
|[Procedimentos armazenados de índice espacial](https://msdn.microsoft.com/library/1be0f34e-3d5a-4a1f-9299-bd482362ec7a)|Usados para analisar e melhorar o desempenho de indexação de índices espaciais.|  
|[Procedimentos armazenados do SQL Server Agent](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)|Usados pelo [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para monitorar o desempenho e a atividade.|  
|[Procedimentos armazenados do SQL Server Profiler](../../relational-databases/system-stored-procedures/sql-server-profiler-stored-procedures-transact-sql.md)|Usados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para gerenciar atividades agendadas e baseadas em eventos.|  
|[Stretch Database procedimentos armazenados](../../relational-databases/system-stored-procedures/stretch-database-extended-stored-procedures-transact-sql.md)|Usado para gerenciar bancos de dados de ampliação.|  
|[Procedimentos armazenados de tabelas temporais](https://msdn.microsoft.com/library/f28ca74e-7876-4592-b794-e78e3690fff6)|Usar para tabelas temporais|  
|[Procedimentos armazenados XML](../../relational-databases/system-stored-procedures/xml-stored-procedures-transact-sql.md)|Usados para gerenciar texto em XML.|  
  
> [!NOTE]  
>  A menos que seja especificamente documentado de outra forma, todos os procedimentos armazenados do sistema retornam o valor 0 para indicar êxito. Para indicar falha, é retornado um valor diferente de zero.  
  
## <a name="api-system-stored-procedures"></a>Procedimentos armazenados do sistema de API  
 Os usuários que executam o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] em aplicativos ADO, OLE DB e ODBC podem perceber que esses aplicativos ao usar procedimentos armazenados do sistema que não foram incluídos na Referência do [!INCLUDE[tsql](../../includes/tsql-md.md)]. Esses procedimentos armazenados são usados pelo [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo e pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC do Native Client para implementar a funcionalidade de uma API de banco de dados. Esses procedimentos armazenados são apenas o mecanismo que o provedor ou o driver utiliza para comunicar as solicitações do usuário a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Eles servem exclusivamente para uso interno do provedor ou do driver. Não há suporte para chamá-los explicitamente de um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aplicativo baseado em um.  
  
 Os procedimentos armazenados sp_createorphan e sp_droporphans são usados para processamento de **imagem** , **texto e Text** **do ODBC.**  
  
 O procedimento armazenado sp_reset_connection é usado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para oferecer suporte a chamadas de procedimento armazenado remoto em uma transação. Esse procedimento armazenado também acionará os eventos de auditoria de logon e de logoff quando uma conexão for reutilizada a partir de um pool de conexões.  
  
 Os procedimentos armazenados do sistema listados nas tabelas a seguir são usados somente em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou por meio de APIs clientes e não se destinam a uso geral pelo clientes. Eles estão sujeitos à alteração e não há garantia de compatibilidade.  
  
 Os procedimentos armazenados a seguir estão documentados nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
|||  
|-|-|  
|sp_catalogs|sp_column_privileges|  
|sp_column_privileges_ex|sp_columns|  
|sp_columns_ex|sp_databases|  
|sp_cursor|sp_cursorclose|  
|sp_cursorexecute|sp_cursorfetch|  
|sp_cursoroption|sp_cursoropen|  
|sp_cursorprepare|sp_cursorprepexec|  
|sp_cursorunprepare|sp_execute|  
|sp_datatype_info|sp_fkeys|  
|sp_foreignkeys|sp_indexes|  
|sp_pkeys|sp_primarykeys|  
|sp_prepare|sp_prepexec|  
|sp_prepexecrpc|sp_unprepare|  
|sp_server_info|sp_special_columns|  
|sp_sproc_columns|sp_statistics|  
|sp_table_privileges|sp_table_privileges_ex|  
|sp_tables|sp_tables_ex|  
  
 Os procedimentos armazenados a seguir não estão documentados:  
  
|||  
|-|-|  
|sp_assemblies_rowset|sp_assemblies_rowset_rmt|  
|sp_assemblies_rowset2|sp_assembly_dependencies_rowset|  
|sp_assembly_dependencies_rowset_rmt|sp_assembly_dependencies_rowset2|  
|sp_bcp_dbcmptlevel|sp_catalogs_rowset|  
|sp_catalogs_rowset;2|sp_catalogs_rowset;5|  
|sp_catalogs_rowset_rmt|sp_catalogs_rowset2|  
|sp_check_constbytable_rowset|sp_check_constbytable_rowset;2|  
|sp_check_constbytable_rowset2|sp_check_constraints_rowset|  
|sp_check_constraints_rowset;2|sp_check_constraints_rowset2|  
|sp_column_privileges_rowset|sp_column_privileges_rowset;2|  
|sp_column_privileges_rowset;5|sp_column_privileges_rowset_rmt|  
|sp_column_privileges_rowset2|sp_columns_90|  
|sp_columns_90_rowset|sp_columns_90_rowset_rmt|  
|sp_columns_90_rowset2|sp_columns_ex_90|  
|sp_columns_rowset|sp_columns_rowset;2|  
|sp_columns_rowset;5|sp_columns_rowset_rmt|  
|sp_columns_rowset2|sp_constr_col_usage_rowset|  
|sp_datatype_info_90|sp_ddopen;1|  
|sp_ddopen;10|sp_ddopen;11|  
|sp_ddopen;12|sp_ddopen;13|  
|sp_ddopen;2|sp_ddopen;3|  
|sp_ddopen;4|sp_ddopen;5|  
|sp_ddopen;6|sp_ddopen;7|  
|sp_ddopen;8|sp_ddopen;9|  
|sp_foreign_keys_rowset|sp_foreign_keys_rowset;2|  
|sp_foreign_keys_rowset;3|sp_foreign_keys_rowset;5|  
|sp_foreign_keys_rowset_rmt|sp_foreign_keys_rowset2|  
|sp_foreign_keys_rowset3|sp_indexes_90_rowset|  
|sp_indexes_90_rowset_rmt|sp_indexes_90_rowset2|  
|sp_indexes_rowset|sp_indexes_rowset;2|  
|sp_indexes_rowset;5|sp_indexes_rowset_rmt|  
|sp_indexes_rowset2|sp_linkedservers_rowset|  
|sp_linkedservers_rowset;2|sp_linkedservers_rowset2|  
|sp_oledb_database|sp_oledb_defdb|  
|sp_oledb_deflang|sp_oledb_language|  
|sp_oledb_ro_usrname|sp_primary_keys_rowset|  
|sp_primary_keys_rowset;2|sp_primary_keys_rowset;3|  
|sp_primary_keys_rowset;5|sp_primary_keys_rowset_rmt|  
|sp_primary_keys_rowset2|sp_procedure_params_90_rowset|  
|sp_procedure_params_90_rowset2|sp_procedure_params_rowset|  
|sp_procedure_params_rowset;2|sp_procedure_params_rowset2|  
|sp_procedures_rowset|sp_procedures_rowset;2|  
|sp_procedures_rowset2|sp_provider_types_90_rowset|  
|sp_provider_types_rowset|sp_schemata_rowset|  
|sp_schemata_rowset;3|sp_special_columns_90|  
|sp_sproc_columns_90|sp_statistics_rowset|  
|sp_statistics_rowset;2|sp_statistics_rowset2|  
|sp_stored_procedures|sp_table_constraints_rowset|  
|sp_table_constraints_rowset;2|sp_table_constraints_rowset2|  
|sp_table_privileges_rowset|sp_table_privileges_rowset;2|  
|sp_table_privileges_rowset;5|sp_table_privileges_rowset_rmt|  
|sp_table_privileges_rowset2|sp_table_statistics_rowset|  
|sp_table_statistics_rowset;2|sp_table_statistics2_rowset|  
|sp_tablecollations|sp_tablecollations_90|  
|sp_tables_info_90_rowset|sp_tables_info_90_rowset_64|  
|sp_tables_info_90_rowset2|sp_tables_info_90_rowset2_64|  
|sp_tables_info_rowset|sp_tables_info_rowset;2|  
|sp_tables_info_rowset_64|sp_tables_info_rowset_64;2|  
|sp_tables_info_rowset2|sp_tables_info_rowset2_64|  
|sp_tables_rowset;2|sp_tables_rowset;5|  
|sp_tables_rowset_rmt|sp_tables_rowset2|  
|sp_usertypes_rowset|sp_usertypes_rowset_rmt|  
|sp_usertypes_rowset2|sp_views_rowset|  
|sp_views_rowset2|sp_xml_schema_rowset|  
|sp_xml_schema_rowset2||  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)   
 [Procedimentos armazenados &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/stored-procedures/stored-procedures-database-engine.md)   
 [Executando procedimentos armazenados &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/stored-procedures-running.md)   
 [Executando procedimentos armazenados](../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md)   
 [Mecanismo de Banco de Dados procedimentos armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [Executando procedimentos armazenados](../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md)  
  
  
