---
title: Gerenciar a coleta de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- data collection [SQL Server]
- data collector [SQL Server], Transact-SQL
- data collector [SQL Server], SQL Server Management Studio
ms.assetid: bc137daa-9f37-4c01-9766-8b7350c75af8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 543f972f5c5805bb1508b6a256f7a7ed3a2aaa3b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62918568"
---
# <a name="manage-data-collection"></a>Gerenciar coleta de dados
  Você pode usar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../includes/tsql-md.md)] procedimentos armazenados e funções para gerenciar diferentes aspectos da coleta de dados, como habilitar ou desabilitar a coleta de dados, alterar a configuração de um conjunto de coleta ou exibir dados no data warehouse de gerenciamento.  
  
## <a name="manage-data-collection-by-using-sql-server-management-studio"></a>Gerenciar a coleta de dados usando o SQL Server Management Studio  
 Você pode executar as seguintes tarefas relacionadas ao coletor de dados usando o Pesquisador de Objetos no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]:  
  
-   [Configurar o Data Warehouse de Gerenciamento &#40;SQL Server Management Studio&#41;](configure-the-management-data-warehouse-sql-server-management-studio.md)  
  
-   [Configurar propriedades de um coletor de dados](configure-properties-of-a-data-collector.md)  
  
-   [Habilitar ou desabilitar a coleta de dados](data-collection.md)  
  
-   [Iniciar ou parar um conjunto de coleta](start-or-stop-a-collection-set.md)  
  
-   [Use SQL Server Profiler para criar um conjunto de coleta de rastreamento do SQL &#40;SQL Server Management Studio&#41;](use-sql-server-profiler-to-create-a-sql-trace-collection-set.md)  
  
-   [Exibir logs do conjunto de coleta &#40;SQL Server Management Studio&#41;](view-collection-set-logs-sql-server-management-studio.md)  
  
-   [Exibir ou alterar agendas do conjunto de coleta &#40;SQL Server Management Studio&#41;](view-or-change-collection-set-schedules-sql-server-management-studio.md)  
  
-   [Exibir um relatório de conjuntos de coleta &#40;SQL Server Management Studio&#41;](view-a-collection-set-report-sql-server-management-studio.md)  
  
## <a name="manage-data-collection-by-using-transact-sql"></a>Gerenciar coleta de dados usando Transact-SQL  
 O coletor de dados fornece uma extensa coleção de procedimentos armazenados que você pode usar para executar qualquer tarefa relacionada ao coletor de dados. Por exemplo, usando o [!INCLUDE[tsql](../../includes/tsql-md.md)], é possível realizar as seguintes tarefas:  
  
-   [Configurar parâmetros de coleta de dados &#40;&#41;Transact-SQL](configure-data-collection-parameters-transact-sql.md)  
  
-   [Habilitar ou desabilitar a coleta de dados](data-collection.md)  
  
-   [Iniciar ou parar um conjunto de coleta](start-or-stop-a-collection-set.md)  
  
-   [Criar um conjunto de coleta personalizado que usa o tipo de coletor de Consultas T-SQL genérico &#40;Transact-SQL&#41;](create-custom-collection-set-generic-t-sql-query-collector-type.md)  
  
-   [Adicionar um item de coleta a um conjunto de coleta &#40;&#41;Transact-SQL](add-a-collection-item-to-a-collection-set-transact-sql.md)  
  
 Além disso, existem funções e exibições que podem ser utilizadas para obter dados de configuração dos bancos de dados msdb e do data warehouse de gerenciamento, dados do log de execução e dados armazenados no data warehouse de gerenciamento.  
  
 Você pode usar os procedimentos armazenados, funções e exibições fornecidos para criar seus próprios cenários de coleta de dados completos.  
  
> [!IMPORTANT]  
>  Diferentemente de procedimentos armazenados regulares, os procedimentos armazenados do coletor de dados usam apenas parâmetros digitados e não oferecem suporte a conversão de tipo de dados automática. Se esses parâmetros não forem chamados pelos tipos de dados com parâmetros de entrada corretos, como especificado na descrição do argumento, o procedimento armazenado retornará um erro.  
  
 Você pode usar o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para criar e executar os códigos de amostra fornecidos. Para obter mais informações, veja [Pesquisador de Objetos](../../ssms/object/object-explorer.md). Como alternativa, você pode criar a consulta em qualquer editor e salvá-la em um arquivo de texto com uma extensão de nome de arquivo .sql. Você pode executar a consulta no prompt de comando do Windows usando o utilitário `sqlcmd`. Para obter mais informações, consulte [usar o utilitário sqlcmd](../scripting/sqlcmd-use-the-utility.md).  
  
### <a name="stored-procedures-and-views"></a>Stored Procedures and Views  
 **Trabalhando com o coletor de dados**  
  
 A tabela a seguir descreve os procedimentos armazenados que podem ser usados para funcionar com o coletor de dados.  
  
|Nome do procedimento|DESCRIÇÃO|  
|--------------------|-----------------|  
|[sp_syscollector_enable_collector](/sql/relational-databases/system-stored-procedures/sp-syscollector-enable-collector-transact-sql)|Habilite o coletor de dados.|  
|[sp_syscollector_disable_collector](/sql/relational-databases/system-stored-procedures/sp-syscollector-disable-collector-transact-sql)|Desabilita o coletor de dados.|  
  
 **Trabalhando com conjuntos de coleta**  
  
 A tabela a seguir descreve os procedimentos armazenados que podem ser usados para funcionar com os conjuntos de coleta.  
  
|Nome do procedimento|DESCRIÇÃO|  
|--------------------|-----------------|  
|[&#41;&#40;Transact-SQL de sp_syscollector_run_collection_set](/sql/relational-databases/system-stored-procedures/sp-syscollector-run-collection-set-transact-sql)|Executar um conjunto de coleta sob demanda.|  
|[&#41;&#40;Transact-SQL de sp_syscollector_start_collection_set](/sql/relational-databases/system-stored-procedures/sp-syscollector-start-collection-set-transact-sql)|Iniciar um conjunto de coleta.|  
|[&#41;&#40;Transact-SQL de sp_syscollector_stop_collection_set](/sql/relational-databases/system-stored-procedures/sp-syscollector-stop-collection-set-transact-sql)|Parar um conjunto de coleta.|  
|[&#41;&#40;Transact-SQL de sp_syscollector_create_collection_set](/sql/relational-databases/system-stored-procedures/sp-syscollector-create-collection-set-transact-sql)|Criar um conjunto de coleta.|  
|[&#41;&#40;Transact-SQL de sp_syscollector_delete_collection_set](/sql/relational-databases/system-stored-procedures/sp-syscollector-delete-collection-set-transact-sql)|Excluir um conjunto de coleta.|  
|[&#41;&#40;Transact-SQL de sp_syscollector_update_collection_set](/sql/relational-databases/system-stored-procedures/sp-syscollector-update-collection-set-transact-sql)|Alterar a configuração de um conjunto de coleta.|  
|[&#41;&#40;Transact-SQL de sp_syscollector_upload_collection_set](/sql/relational-databases/system-stored-procedures/sp-syscollector-upload-collection-set-transact-sql)|Carregar dados de um conjunto de coleta no data warehouse de gerenciamento. Isso é efetivamente um carregamento sob demanda.|  
  
 **Trabalhando com itens de coleta**  
  
 A tabela a seguir descreve os procedimentos armazenados que podem ser usados para funcionar com os itens de coleta.  
  
|Nome do procedimento|DESCRIÇÃO|  
|--------------------|-----------------|  
|[&#41;&#40;Transact-SQL de sp_syscollector_create_collection_item](/sql/relational-databases/system-stored-procedures/sp-syscollector-create-collection-item-transact-sql)|Criar um item de coleta.|  
|[&#41;&#40;Transact-SQL de sp_syscollector_delete_collection_item](/sql/relational-databases/system-stored-procedures/sp-syscollector-delete-collection-item-transact-sql)|Excluir um item de coleta.|  
|[&#41;&#40;Transact-SQL de sp_syscollector_update_collection_item](/sql/relational-databases/system-stored-procedures/sp-syscollector-update-collection-item-transact-sql)|Atualizar um item de coleta.|  
  
 **Trabalhando com tipos de coletor**  
  
 A tabela a seguir descreve os procedimentos armazenados que podem ser usados para funcionar com os tipos de coletor.  
  
|Nome do procedimento|DESCRIÇÃO|  
|--------------------|-----------------|  
|[&#41;&#40;Transact-SQL de sp_syscollector_create_collector_type](/sql/relational-databases/system-stored-procedures/sp-syscollector-create-collector-type-transact-sql)|Criar um tipo de coletor.|  
|[&#41;&#40;Transact-SQL de sp_syscollector_update_collector_type](/sql/relational-databases/system-stored-procedures/sp-syscollector-update-collector-type-transact-sql)|Atualizar um tipo de coletor.|  
|[&#41;&#40;Transact-SQL de sp_syscollector_delete_collector_type](/sql/relational-databases/system-stored-procedures/sp-syscollector-delete-collector-type-transact-sql)|Exclui um tipo de coletor.|  
  
 **Obtendo informações de configuração**  
  
 A tabela a seguir descreve as exibições que podem ser usadas para se obter informações de configuração e dados do log de execução.  
  
|Nome da exibição|DESCRIÇÃO|  
|---------------|-----------------|  
|[&#41;&#40;Transact-SQL de syscollector_config_store](/sql/relational-databases/system-catalog-views/syscollector-config-store-transact-sql)|Obter configuração do coletor de dados.|  
|[&#41;&#40;Transact-SQL de syscollector_collection_items](/sql/relational-databases/system-catalog-views/syscollector-collection-items-transact-sql)|Obter informações sobre o item de coleta.|  
|[&#41;&#40;Transact-SQL de syscollector_collection_sets](/sql/relational-databases/system-catalog-views/syscollector-collection-sets-transact-sql)|Obter informações sobre o conjunto de coleta.|  
|[&#41;&#40;Transact-SQL de syscollector_collector_types](/sql/relational-databases/system-catalog-views/syscollector-collector-types-transact-sql)|Obter informações sobre o tipo de coletor.|  
|[&#41;&#40;Transact-SQL de syscollector_execution_log](/sql/relational-databases/system-catalog-views/syscollector-execution-log-transact-sql)|Obter informações sobre o conjunto de coleta e a execução do pacote.|  
|[&#41;&#40;Transact-SQL de syscollector_execution_stats](/sql/relational-databases/system-catalog-views/syscollector-execution-stats-transact-sql)|Obter informações sobre a execução de tarefa.|  
|[&#41;&#40;Transact-SQL de syscollector_execution_log_full](/sql/relational-databases/system-catalog-views/syscollector-execution-log-full-transact-sql)|Obter informações quando o log de execução estiver completo.|  
  
 **Configurando o acesso ao data warehouse de gerenciamento**  
  
 A tabela a seguir descreve os procedimentos armazenados que podem ser usados para configurar o acesso ao data warehouse de gerenciamento.  
  
|Nome do procedimento|DESCRIÇÃO|  
|--------------------|-----------------|  
|[&#41;&#40;Transact-SQL de sp_syscollector_set_warehouse_database_name](/sql/relational-databases/system-stored-procedures/sp-syscollector-set-warehouse-database-name-transact-sql)|Especificar o nome de banco de dados definido na cadeia de caracteres de conexão para o data warehouse de gerenciamento.|  
|[&#41;&#40;Transact-SQL de sp_syscollector_set_warehouse_instance_name](/sql/relational-databases/system-stored-procedures/sp-syscollector-set-warehouse-instance-name-transact-sql)|Especificar a instância definida na cadeia de caracteres de conexão para o data warehouse de gerenciamento.|  
  
 **Configurando o data warehouse de gerenciamento**  
  
 A tabela a seguir descreve os procedimentos armazenados que podem ser usados para funcionar com a configuração do data warehouse de gerenciamento.  
  
|Nome do procedimento|DESCRIÇÃO|  
|--------------------|-----------------|  
|[Core. sp_create_snapshot &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/core-sp-create-snapshot-transact-sql)|Criar um instantâneo de coleta no data warehouse de gerenciamento.|  
|[Core. sp_update_data_source &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/core-sp-update-data-source-transact-sql)|Atualizar a fonte de dados para coleta de dados.|  
|[Core. sp_add_collector_type &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/core-sp-add-collector-type-transact-sql)|Adicionar um tipo de coletor ao data warehouse de gerenciamento.|  
|[Core. sp_remove_collector_type &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/core-sp-remove-collector-type-transact-sql)|Remover um tipo de coletor do data warehouse de gerenciamento.|  
|[Core. sp_purge_data &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/core-sp-purge-data-transact-sql)|Excluir dados do data warehouse de gerenciamento.|  
  
 **Trabalhando com pacotes de carregamento**  
  
 A tabela a seguir descreve os procedimentos armazenados que podem ser usados para funcionar com pacotes de carregamento.  
  
|Nome do procedimento|DESCRIÇÃO|  
|--------------------|-----------------|  
|[&#41;&#40;Transact-SQL de sp_syscollector_set_cache_window](/sql/relational-databases/system-stored-procedures/sp-syscollector-set-cache-window-transact-sql)|Configurar o número de repetições do carregamento de dados.|  
|[&#41;&#40;Transact-SQL de sp_syscollector_set_cache_directory](/sql/relational-databases/system-stored-procedures/sp-syscollector-set-cache-directory-transact-sql)|Especificar o armazenamento temporário entre as repetições de carregamento.|  
  
 **Trabalhando com o log de execução de coleta de dados**  
  
 A tabela a seguir descreve os procedimentos armazenados que podem ser usados para funcionar com o log de execução de coleta de dados.  
  
|Nome do procedimento|DESCRIÇÃO|  
|--------------------|-----------------|  
|[&#41;&#40;Transact-SQL de sp_syscollector_delete_execution_log_tree](/sql/relational-databases/system-stored-procedures/sp-syscollector-delete-execution-log-tree-transact-sql)|Excluir entradas do conjunto de coleta do log de execução.|  
  
### <a name="functions"></a>Funções  
 A tabela a seguir descreve as funções que podem ser usadas para obter informações de execução e rastreamento.  
  
|Nome da função|DESCRIÇÃO|  
|-------------------|-----------------|  
|[&#41;&#40;Transact-SQL de fn_syscollector_get_execution_details](/sql/relational-databases/system-functions/fn-syscollector-get-execution-details-transact-sql)|Obter os dados de log de execução do [!INCLUDE[ssIS](../../includes/ssis-md.md)] para um pacote específico.|  
|[&#41;&#40;Transact-SQL de fn_syscollector_get_execution_stats](/sql/relational-databases/system-functions/fn-syscollector-get-execution-stats-transact-sql)|Obter estatísticas de execução para um pacote ou conjunto de coleta. Estas informações incluem erros que estão registrados.|  
|[instantâneos. fn_trace_getdata &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/snapshots-fn-trace-getdata-transact-sql)|Obter os eventos que são registrados quando o tipo de coletor de Rastreamento do SQL Genérico é usado para coletar dados.|  
  
## <a name="see-also"></a>Consulte Também  
 [Executar um procedimento armazenado](../stored-procedures/execute-a-stored-procedure.md)   
 [Usar SQL Server Management Studio](../../database-engine/use-sql-server-management-studio.md)   
 [Coleta de dados](data-collection.md)  
  
  
