---
description: Gerenciar coleta de dados
title: Gerenciar a coleta de dados | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
keywords:
- Coleta de dados
helpviewer_keywords:
- data collection [SQL Server]
- data collector [SQL Server], Transact-SQL
- data collector [SQL Server], SQL Server Management Studio
ms.assetid: bc137daa-9f37-4c01-9766-8b7350c75af8
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 754aff825e0da8fd888deafb927936599a4d8631
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92196760"
---
# <a name="manage-data-collection"></a>Gerenciar coleta de dados
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
 Use os procedimentos armazenados e as funções do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../includes/tsql-md.md)] para gerenciar diferentes aspectos da coleta de dados, como habilitar ou desabilitar a coleta de dados, alterar a configuração de um conjunto de coleta ou exibir dados no data warehouse de gerenciamento.  
  
## <a name="manage-data-collection-using-ssms"></a>Gerenciar coleta de dados usando o SSMS  
 Execute as seguintes tarefas relacionadas ao coletor de dados usando o Pesquisador de Objetos no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]:  
  
-   [Configurar o Data Warehouse de Gerenciamento &#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/configure-the-management-data-warehouse-sql-server-management-studio.md)  
  
-   [Configurar propriedades de um coletor de dados](../../relational-databases/data-collection/configure-properties-of-a-data-collector.md)  
  
-   [Habilitar ou desabilitar a coleta de dados](../../relational-databases/data-collection/enable-or-disable-data-collection.md)  
  
-   [Iniciar ou interromper um conjunto de coleta](../../relational-databases/data-collection/start-or-stop-a-collection-set.md)  
  
-   [Usar o SQL Server Profiler para criar um conjunto de coleta de Rastreamento do SQL &#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/use-sql-server-profiler-to-create-a-sql-trace-collection-set.md)  
  
-   [Exibir logs de conjuntos de coleta &#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/view-collection-set-logs-sql-server-management-studio.md)  
  
-   [Exibir ou alterar agendas de conjuntos de coleta &#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/view-or-change-collection-set-schedules-sql-server-management-studio.md)  
  
-   [Exibir um relatório de conjuntos de coleta &#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/view-a-collection-set-report-sql-server-management-studio.md)  
  
## <a name="manage-data-collection-using-transact-sql"></a>Gerenciar a coleta de dados usando Transact-SQL  
 O coletor de dados fornece uma extensa coleção de procedimentos armazenados que você pode usar para executar qualquer tarefa relacionada ao coletor de dados. Por exemplo, usando o [!INCLUDE[tsql](../../includes/tsql-md.md)], é possível realizar as seguintes tarefas:  
  
-   [Configurar parâmetros de coleta de dados &#40;Transact-SQL&#41;](../../relational-databases/data-collection/configure-data-collection-parameters-transact-sql.md)  
  
-   [Habilitar ou desabilitar a coleta de dados](../../relational-databases/data-collection/enable-or-disable-data-collection.md)  
  
-   [Iniciar ou interromper um conjunto de coleta](../../relational-databases/data-collection/start-or-stop-a-collection-set.md)  
  
-   [Criar um conjunto de coleta personalizado que usa o tipo de coletor de Consultas T-SQL genérico &#40;Transact-SQL&#41;](../../relational-databases/data-collection/create-custom-collection-set-generic-t-sql-query-collector-type.md)  
  
-   [Adicionar um item de coleta a um conjunto de coletas &#40;Transact-SQL&#41;](../../relational-databases/data-collection/add-a-collection-item-to-a-collection-set-transact-sql.md)  
  
 Além disso, existem funções e exibições que podem ser utilizadas para obter dados de configuração dos bancos de dados msdb e do data warehouse de gerenciamento, dados do log de execução e dados armazenados no data warehouse de gerenciamento.  
  
 Você pode usar os procedimentos armazenados, funções e exibições fornecidos para criar seus próprios cenários de coleta de dados completos.  
  
>**IMPORTANTE:** Diferentemente de procedimentos armazenados regulares, os procedimentos armazenados do coletor de dados usam apenas parâmetros digitados e não oferecem suporte a conversão de tipo de dados automática. Se esses parâmetros não forem chamados pelos tipos de dados com parâmetros de entrada corretos, como especificado na descrição do argumento, o procedimento armazenado retornará um erro.  
  
 Use o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para criar e executar os exemplos de código fornecidos. Para obter mais informações, veja [Pesquisador de Objetos](../../ssms/object/object-explorer.md). Como alternativa, você pode criar a consulta em qualquer editor e salvá-la em um arquivo de texto com uma extensão de nome de arquivo .sql. Você pode executar a consulta no prompt de comando do Windows usando o utilitário **sqlcmd** . Para obter mais informações, consulte [Usar o Utilitário sqlcmd](../../ssms/scripting/sqlcmd-use-the-utility.md).  
  
### <a name="stored-procedures-and-views"></a>Stored Procedures and Views  
 **Trabalhando com o coletor de dados**  
  
 A tabela a seguir descreve os procedimentos armazenados que podem ser usados para funcionar com o coletor de dados.  
  
|Nome do procedimento|Descrição|  
|--------------------|-----------------|  
|[sp_syscollector_enable_collector](../../relational-databases/system-stored-procedures/sp-syscollector-enable-collector-transact-sql.md)|Habilite o coletor de dados.|  
|[sp_syscollector_disable_collector](../../relational-databases/system-stored-procedures/sp-syscollector-disable-collector-transact-sql.md)|Desabilita o coletor de dados.|  
  
 **Trabalhando com conjuntos de coleta**  
  
 A tabela a seguir descreve os procedimentos armazenados que podem ser usados para funcionar com os conjuntos de coleta.  
  
|Nome do procedimento|Descrição|  
|--------------------|-----------------|  
|[sp_syscollector_run_collection_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-run-collection-set-transact-sql.md)|Executar um conjunto de coleta sob demanda.|  
|[sp_syscollector_start_collection_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-start-collection-set-transact-sql.md)|Iniciar um conjunto de coleta.|  
|[sp_syscollector_stop_collection_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-stop-collection-set-transact-sql.md)|Parar um conjunto de coleta.|  
|[sp_syscollector_create_collection_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-set-transact-sql.md)|Criar um conjunto de coleta.|  
|[sp_syscollector_delete_collection_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-delete-collection-set-transact-sql.md)|Excluir um conjunto de coleta.|  
|[sp_syscollector_update_collection_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-update-collection-set-transact-sql.md)|Alterar a configuração de um conjunto de coleta.|  
|[sp_syscollector_upload_collection_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-upload-collection-set-transact-sql.md)|Carregar dados de um conjunto de coleta no data warehouse de gerenciamento. Isso é efetivamente um carregamento sob demanda.|  
  
 **Trabalhando com itens de coleta**  
  
 A tabela a seguir descreve os procedimentos armazenados que podem ser usados para funcionar com os itens de coleta.  
  
|Nome do procedimento|Descrição|  
|--------------------|-----------------|  
|[sp_syscollector_create_collection_item &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-item-transact-sql.md)|Criar um item de coleta.|  
|[sp_syscollector_delete_collection_item &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-delete-collection-item-transact-sql.md)|Excluir um item de coleta.|  
|[sp_syscollector_update_collection_item &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-update-collection-item-transact-sql.md)|Atualizar um item de coleta.|  
  
 **Trabalhando com tipos de coletor**  
  
 A tabela a seguir descreve os procedimentos armazenados que podem ser usados para funcionar com os tipos de coletor.  
  
|Nome do procedimento|Descrição|  
|--------------------|-----------------|  
|[sp_syscollector_create_collector_type &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collector-type-transact-sql.md)|Criar um tipo de coletor.|  
|[sp_syscollector_update_collector_type &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-update-collector-type-transact-sql.md)|Atualizar um tipo de coletor.|  
|[sp_syscollector_delete_collector_type &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-delete-collector-type-transact-sql.md)|Exclui um tipo de coletor.|  
  
 **Obtendo informações de configuração**  
  
 A tabela a seguir descreve as exibições que podem ser usadas para se obter informações de configuração e dados do log de execução.  
  
|Nome da exibição|Descrição|  
|---------------|-----------------|  
|[syscollector_config_store &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-config-store-transact-sql.md)|Obter configuração do coletor de dados.|  
|[syscollector_collection_items &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collection-items-transact-sql.md)|Obter informações sobre o item de coleta.|  
|[syscollector_collection_sets &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collection-sets-transact-sql.md)|Obter informações sobre o conjunto de coleta.|  
|[syscollector_collector_types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collector-types-transact-sql.md)|Obter informações sobre o tipo de coletor.|  
|[syscollector_execution_log &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-execution-log-transact-sql.md)|Obter informações sobre o conjunto de coleta e a execução do pacote.|  
|[syscollector_execution_stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-execution-stats-transact-sql.md)|Obter informações sobre a execução de tarefa.|  
|[syscollector_execution_log_full &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-execution-log-full-transact-sql.md)|Obter informações quando o log de execução estiver completo.|  
  
 **Configurando o acesso ao data warehouse de gerenciamento**  
  
 A tabela a seguir descreve os procedimentos armazenados que podem ser usados para configurar o acesso ao data warehouse de gerenciamento.  
  
|Nome do procedimento|Descrição|  
|--------------------|-----------------|  
|[sp_syscollector_set_warehouse_database_name &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-set-warehouse-database-name-transact-sql.md)|Especificar o nome de banco de dados definido na cadeia de caracteres de conexão para o data warehouse de gerenciamento.|  
|[sp_syscollector_set_warehouse_instance_name &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-set-warehouse-instance-name-transact-sql.md)|Especificar a instância definida na cadeia de caracteres de conexão para o data warehouse de gerenciamento.|  
  
 **Configurando o data warehouse de gerenciamento**  
  
 A tabela a seguir descreve os procedimentos armazenados que podem ser usados para funcionar com a configuração do data warehouse de gerenciamento.  
  
|Nome do procedimento|Descrição|  
|--------------------|-----------------|  
|[core.sp_create_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/core-sp-create-snapshot-transact-sql.md)|Criar um instantâneo de coleta no data warehouse de gerenciamento.|  
|[core.sp_update_data_source &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/core-sp-update-data-source-transact-sql.md)|Atualizar a fonte de dados para coleta de dados.|  
|[core.sp_add_collector_type &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/core-sp-add-collector-type-transact-sql.md)|Adicionar um tipo de coletor ao data warehouse de gerenciamento.|  
|[core.sp_remove_collector_type &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/core-sp-remove-collector-type-transact-sql.md)|Remover um tipo de coletor do data warehouse de gerenciamento.|  
|[core.sp_purge_data &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/core-sp-purge-data-transact-sql.md)|Excluir dados do data warehouse de gerenciamento.|  
  
 **Trabalhando com pacotes de carregamento**  
  
 A tabela a seguir descreve os procedimentos armazenados que podem ser usados para funcionar com pacotes de carregamento.  
  
|Nome do procedimento|Descrição|  
|--------------------|-----------------|  
|[sp_syscollector_set_cache_window &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-set-cache-window-transact-sql.md)|Configurar o número de repetições do carregamento de dados.|  
|[sp_syscollector_set_cache_directory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-set-cache-directory-transact-sql.md)|Especificar o armazenamento temporário entre as repetições de carregamento.|  
  
 **Trabalhando com o log de execução de coleta de dados**  
  
 A tabela a seguir descreve os procedimentos armazenados que podem ser usados para funcionar com o log de execução de coleta de dados.  
  
|Nome do procedimento|Descrição|  
|--------------------|-----------------|  
|[sp_syscollector_delete_execution_log_tree &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-delete-execution-log-tree-transact-sql.md)|Excluir entradas do conjunto de coleta do log de execução.|  
  
### <a name="functions"></a>Funções  
 A tabela a seguir descreve as funções que podem ser usadas para obter informações de execução e rastreamento.  
  
|Nome da função|Descrição|  
|-------------------|-----------------|  
|[fn_syscollector_get_execution_details &#40;Transact-SQL&#41;](../../relational-databases/system-functions/fn-syscollector-get-execution-details-transact-sql.md)|Obter os dados de log de execução do [!INCLUDE[ssIS](../../includes/ssis-md.md)] para um pacote específico.|  
|[fn_syscollector_get_execution_stats &#40;Transact-SQL&#41;](../../relational-databases/system-functions/fn-syscollector-get-execution-stats-transact-sql.md)|Obter estatísticas de execução para um pacote ou conjunto de coleta. Estas informações incluem erros que estão registrados.|  
|[snapshots.fn_trace_getdata &#40;Transact-SQL&#41;](../../relational-databases/system-functions/snapshots-fn-trace-getdata-transact-sql.md)|Obter os eventos que são registrados quando o tipo de coletor de Rastreamento do SQL Genérico é usado para coletar dados.|  
  
## <a name="see-also"></a>Confira também  
 [Executar um procedimento armazenado](../../relational-databases/stored-procedures/execute-a-stored-procedure.md)   
 [Usar o SQL Server Management Studio](../../ssms/sql-server-management-studio-ssms.md)   
 [Coleta de Dados](../../relational-databases/data-collection/data-collection.md)  
  
