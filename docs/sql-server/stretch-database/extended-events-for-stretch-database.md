---
description: Eventos Estendidos para o Stretch Database
title: Eventos Estendidos para o Stretch Database
ms.date: 06/14/2016
ms.service: sql-server-stretch-database
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 70485e74-2e25-4e7e-be6c-9dd1780a42e3
author: rothja
ms.author: jroth
ms.custom: seo-dt-2019
ms.openlocfilehash: 02fe62db4f59916f5b97624c4b4560a33738d761
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88454336"
---
# <a name="extended-events-for-stretch-database"></a>Eventos Estendidos para o Stretch Database
[!INCLUDE [sqlserver2016-windows-only](../../includes/applies-to-version/sqlserver2016-windows-only.md)]


O Stretch Database fornece um conjunto de eventos estendidos para solução de problemas.  
  
Para obter mais informações, veja [Eventos Estendidos](../../relational-databases/extended-events/extended-events.md). Para obter informações sobre como iniciar uma sessão de eventos estendidos para solução de problemas, veja [Criar uma sessão de Eventos Estendidos](https://msdn.microsoft.com/library/34b1e95a-a80e-4aca-9201-abde47f2ca74)  
  
## <a name="list-of-extended-events-for-stretch-database"></a>Lista de eventos estendidos para o Stretch Database  
  
Nome do evento|Descrição do evento   
---------|---------  
remote_data_archive_db_ddl|Ocorre quando o ddl T-SQL do banco de dados para transferir dados é processado.  
remote_data_archive_provision_operation|Ocorre quando uma operação de provisionamento é iniciada ou encerrada.  
remote_data_archive_query_rewrite|Ocorre quando RelOp_Get é substituído durante a regravação da consulta no Stretch.  
remote_data_archive_table_ddl|Ocorre quando o ddl T-SQL da tabela para transferir dados é processado.  
remote_data_archive_telemetry|Ocorre sempre quando um sistema local transmite um evento de telemetria para o Banco de Dados do Azure.  
remote_data_archive_telemetry_rejected|Ocorre sempre que um evento de telemetria de um Stretch Database do Azure é rejeitado  
repopulate_stretch_schema_task_queue_complete|Relata a conclusão da repopulação da fila de tarefas do esquema de transferência.  
repopulate_stretch_schema_task_queue_start|Relata o início da repopulação da fila de tarefas do esquema de ampliação.  
stretch_codegen_errorlog|Relata a saída do gerador de código  
stretch_codegen_start|Relata o início da geração de código de transferência  
stretch_create_remote_table_start|Relata o início da criação da tabela remota  
stretch_database_disable_completed|Relata a conclusão de um comando ALTER DATABASE SET REMOTE_DATA_ARCHIVE OFF  
stretch_database_enable_completed|Relata a conclusão de um comando ALTER DATABASE SET REMOTE_DATA_ARCHIVE ON  
stretch_database_reauthorize_completed|Relata a conclusão de um procedimento especial sp_rda_reauthorize_db  
stretch_index_reconciliation_codegen_completed|Relata a conclusão da geração de código para a operação de ampliar índice remoto  
stretch_index_update_step_completed|Relata a duração da operação de atualização do índice estendido  
stretch_migration_debug_trace|Rastreamento de depuração das ações de migração de transferência.  
stretch_migration_dequeue_migration|Evento gerado quando uma tarefa de migração de ampliação é retirada da fila para um banco de dados.  
stretch_migration_queue_migration|Coloque um pacote na fila para começar a migração do banco de dados e objeto.  
stretch_migration_requeue_migration|Evento gerado quando um pacote de tarefa de migração de ampliação é recolocado na fila.  
stretch_migration_start_migration|Inicie a migração do banco de dados e objeto.  
stretch_migration_start_unmigration|Inicie a reversão da migração do banco de dados e objeto.  
stretch_remote_column_execution_completed|Relata a conclusão da execução remota para o código gerado para uma coluna transferida  
stretch_remote_column_reconciliation_codegen_completed|Relata a conclusão da geração de código para a reconciliação da coluna remota ampliada  
stretch_remote_index_execution_completed|Relata a conclusão da execução remota para o código gerado para um índice estendido  
stretch_schema_queue_task|Relata quando um pacote está prestes a entrar na fila para processar uma tarefa de esquema para o banco de dados e objeto.  
stretch_schema_script_execution_completed|Relata a conclusão da execução do script de ampliação durante o processamento de tarefa do esquema de ampliação.  
stretch_schema_script_execution_skipped|Relata ignorar a execução do script de ampliação durante o processamento de tarefa do esquema de ampliação.  
stretch_schema_script_execution_start|Relata o início da execução do script de ampliação durante o processamento de tarefa do esquema de ampliação.  
stretch_schema_task_failed|Relata a falha de uma função do esquema de ampliação durante a tarefa do esquema de ampliação.  
stretch_schema_task_skipped|Relata que a tarefa de esquema de ampliação é ignorada durante a função do esquema de ampliação.  
stretch_schema_task_start|Relata o início da função de estender o esquema durante a tarefa de estender o esquema.  
stretch_schema_task_succeeded|Relata a conclusão com êxito da função do esquema de ampliação durante a tarefa do esquema de ampliação.  
stretch_sp_migration_get_batch_id|Chamar sp_stretch_get_batch_id  
stretch_sync_metadata_start|Relata o início da verificação de metadados durante a tarefa de migração.  
stretch_table_codegen_completed|Relata a conclusão da geração do código para uma tabela transferida  
stretch_table_complete_data_reconciliation|Conclua a reconciliação de dados do banco de dados e do objeto.  
stretch_table_data_reconciliation_event|Relata a conclusão de uma reconciliação de dados de um lote de linhas  
stretch_table_data_reconciliation_results_event|Relata um erro ou uma conclusão de uma reconciliação de dados bem-sucedida de um número de lotes de linhas  
stretch_table_hinted_admin_delete_event|Relata a execução de uma operação DML de exclusão do Stretch que usa uma dica do administrador  
stretch_table_hinted_admin_update_event|Relata a execução de uma operação DML de atualização do Stretch que usa uma dica do administrador  
stretch_table_provisioning_step_completed|Relata a duração de uma operação de provisionamento de tabela transferida  
stretch_table_query_error|Relata um erro lançado durante a regravação da consulta do Stretch  
stretch_table_remote_creation_completed|Relata a conclusão da execução remota para o código gerado para uma tabela transferida  
stretch_table_row_migration_event|Relata a conclusão da migração de um lote de linhas  
stretch_table_row_migration_results_event|Relata um erro ou conclusão de uma migração bem-sucedida de um número de lotes de linhas  
stretch_table_row_unmigration_event|Relata a conclusão do cancelamento de migração de um lote de linhas  
stretch_table_row_unmigration_results_event|Relata um erro ou a conclusão de uma reversão de migração com êxito de diversos lotes de linhas  
stretch_table_start_data_reconciliation|Inicie a reconciliação de dados do banco de dados e do objeto.  
stretch_table_unprovision_completed|Relata a conclusão da remoção dos recursos locais para uma tabela que não foi transferida  
stretch_table_validation_error|Relata a conclusão da validação para uma tabela quando o usuário habilita a ampliação  
stretch_unprovision_table_start|Relata o início do cancelamento do provisionamento da tabela de ampliação  
  
## <a name="see-also"></a>Consulte Também  
[Gerenciar e solucionar problemas do Stretch Database](../../sql-server/stretch-database/manage-and-troubleshoot-stretch-database.md)  

