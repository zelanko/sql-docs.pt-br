---
title: sys. dm_db_xtp_checkpoint_files (Transact-SQL) | Microsoft Docs
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.custom: ''
ms.technology: in-memory-oltp
ms.topic: language-reference
f1_keywords:
- dm_db_xtp_checkpoint_files
- sys.dm_db_xtp_checkpoint_files_TSQL
- dm_db_xtp_checkpoint_files_TSQL
- sys.dm_db_xtp_checkpoint_files
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_xtp_checkpoint_files dynamic management view
ms.assetid: ac8e6333-7a9f-478a-b446-5602283e81c9
author: stevestein
ms.author: sstein
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: fb3aa62880de7013cf503e61eb2d86a3454c2350
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68026913"
---
# <a name="sysdm_db_xtp_checkpoint_files-transact-sql"></a>sys.dm_db_xtp_checkpoint_files (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  Exibe informações sobre os arquivos de ponto de verificação, incluindo o tamanho do arquivo, o local físico e a ID da transação.  
  
> **Observação:** Para o ponto de verificação atual que não foi fechado, a coluna State`ys.dm_db_xtp_checkpoint_files` de s estará em construção para novos arquivos. Um ponto de verificação é fechado automaticamente quando há um crescimento de log de transações suficiente desde o último ponto de `CHECKPOINT` verificação ou se você emitir o comando ([ponto de verificação &#40;&#41;Transact-SQL ](../../t-sql/language-elements/checkpoint-transact-sql.md)).  
  
 Um grupo de arquivos com otimização de memória usa internamente arquivos somente de acréscimo para armazenar linhas inseridas e excluídas para tabelas na memória. Existem dois tipos de arquivos. Um arquivo de dados contém linhas inseridas enquanto um arquivo Delta contém referências a linhas excluídas. 
  
 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]é substancialmente diferente das versões mais recentes e é discutido no tópico em [SQL Server 2014](#bkmk_2014).  
  
 Para obter mais informações, consulte [criando e gerenciando armazenamento para objetos com otimização de memória](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md).  
  
##  <a name="bkmk_2016"></a>[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior  
 A tabela a seguir descreve as colunas `sys.dm_db_xtp_checkpoint_files`do, começando **[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]** com.  
  
|Nome da coluna|Type|DESCRIÇÃO|  
|-----------------|----------|-----------------|  
|container_id|**int**|A ID do contêiner (representado como um arquivo com o tipo FILESTREAM em sys.database_files) da qual fazem parte os dados ou o arquivo delta. Junções com file_id em [Sys. database_files &#40;&#41;do Transact-SQL ](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md).|  
|container_guid|**uniqueidentifier**|GUID do contêiner, do qual a raiz, os dados ou o arquivo Delta fazem parte. Une-se com file_guid na tabela sys. database_files.|  
|checkpoint_file_id|**uniqueidentifier**|GUID do arquivo de ponto de verificação.|  
|relative_file_path|**nvarchar(256)**|Caminho do arquivo relativo ao contêiner ao qual está mapeado.|  
|file_type|**smallint**|-1 gratuitamente<br /><br /> 0 para arquivo de dados.<br /><br /> 1 para arquivo DELTA.<br /><br /> 2 para o arquivo raiz<br /><br /> 3 para arquivo de dados grandes|  
|file_type_desc|**nvarchar (60)**|LIVRE-todos os arquivos mantidos como livres estão disponíveis para alocação. Os arquivos gratuitos podem variar em tamanho, dependendo das necessidades antecipadas pelo sistema. O tamanho máximo é 1GB.<br /><br /> Os arquivos de dados de dados contêm linhas que foram inseridas em tabelas com otimização de memória.<br /><br /> Os arquivos Delta-Delta contêm referências a linhas em arquivos de dados que foram excluídos.<br /><br /> Os arquivos raiz raiz contêm metadados do sistema para objetos com otimização de memória e compilados nativamente.<br /><br /> DADOS grandes-os arquivos de dados grandes contêm valores inseridos nas colunas (n) varchar (max) e varbinary (max), bem como os segmentos de coluna que fazem parte dos índices columnstore em tabelas com otimização de memória.|  
|internal_storage_slot|**int**|O índice do arquivo na matriz de armazenamento interna. NULO para raiz ou para outro estado diferente de 1.|  
|checkpoint_pair_file_id|**uniqueidentifier**|DADOS correspondentes ou arquivo DELTA. NULO para raiz.|  
|file_size_in_bytes|**bigint**|Tamanho do arquivo no disco.|  
|file_size_used_in_bytes|**bigint**|Para os pares de arquivos de ponto de verificação que ainda estão sendo populados, essa coluna será atualizada após o próximo ponto de verificação.|  
|logical_row_count|**bigint**|Para dados, número de linhas inseridas.<br /><br /> Para o Delta, o número de linhas excluídas após a contabilidade para DROP TABLE.<br /><br /> Para root, NULL.|  
|state|**smallint**|0-CRIADO<br /><br /> 1-EM CONSTRUÇÃO<br /><br /> 2 - ATIVO<br /><br /> 3-DESTINO DE MESCLAGEM<br /><br /> 8-AGUARDANDO TRUNCAMENTO DE LOG|  
|state_desc|**nvarchar (60)**|Pré-criado-um número de arquivos de ponto de verificação é pré-alocado para minimizar ou eliminar as esperas para alocar novos arquivos à medida que as transações são executadas. Esses arquivos criados podem variar em tamanho, dependendo das necessidades estimadas da carga de trabalho, mas não contêm dados. Essa é uma sobrecarga de armazenamento em bancos de dados com um grupo de arquivos MEMORY_OPTIMIZED_DATA.<br /><br /> EM construção-esses arquivos de ponto de verificação estão em construção, o que significa que eles estão sendo preenchidos com base nos registros de log gerados pelo banco de dados e ainda não fazem parte de um ponto de verificação.<br /><br /> ATIVO-contém as linhas inseridas/excluídas dos pontos de verificação fechados anteriores. Eles contêm o conteúdo das tabelas que a área lê na memória antes de aplicar a parte ativa do log de transações na reinicialização do banco de dados. Esperamos que esse tamanho desses arquivos de ponto de verificação seja aproximadamente 2x do tamanho da memória das tabelas com otimização de memória, supondo que a operação de mesclagem esteja acompanhando a carga de trabalho transacional.<br /><br /> DESTINO de MESCLAgem-o destino de operações de mesclagem – esses arquivos de ponto de verificação armazenam as linhas de dados consolidadas dos arquivos de origem que foram identificados pela política de mesclagem. Assim que a mesclagem for instalada, a opção MESCLAR DESTINO entrará no estado ATIVO.<br /><br /> AGUARDAndo TRUNCAmento de LOG-depois que a mesclagem tiver sido instalada e o CFP de destino de MESCLAgem fizer parte do ponto de verificação durável, os arquivos de ponto de verificação de origem de mesclagem serão transferidos para esse estado. Os arquivos nesse estado são necessários para a exatidão operacional do banco de dados com a tabela com otimização de memória.  Por exemplo, restaurar de um ponto de verificação durável para voltar no tempo.|  
|lower_bound_tsn|**bigint**|Limite inferior da transação no arquivo; NULL se o estado não estiver em (1, 3).|  
|upper_bound_tsn|**bigint**|Limite superior da transação no arquivo; NULL se o estado não estiver em (1, 3).|  
|begin_checkpoint_id|**bigint**|ID do ponto de verificação de início.|  
|end_checkpoint_id|**bigint**|ID do ponto de verificação final.|  
|last_updated_checkpoint_id|**bigint**|ID do último ponto de verificação que atualizou este arquivo.|  
|encryption_status|**smallint**|0, 1, 2|  
|encryption_status_desc|**nvarchar (60)**|0 => UNENCRTPTED<br /><br /> 1 => CRIPTOGRAFADO COM A CHAVE 1<br /><br /> 2 => CRIPTOGRAFADO COM A CHAVE 2. Válido somente para arquivos ativos.|  
  
##  <a name="bkmk_2014"></a> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
 A tabela a seguir descreve as colunas `sys.dm_db_xtp_checkpoint_files`para, **[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]** para.  
  
|Nome da coluna|Type|DESCRIÇÃO|  
|-----------------|----------|-----------------|  
|container_id|**int**|A ID do contêiner (representado como um arquivo com o tipo FILESTREAM em sys.database_files) da qual fazem parte os dados ou o arquivo delta. Junções com file_id em [Sys. database_files &#40;&#41;do Transact-SQL ](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md).|  
|container_guid|**uniqueidentifier**|O GUID do contêiner do qual fazem parte os dados ou o arquivo delta.|  
|checkpoint_file_id|**GUID**|ID dos dados ou arquivo delta.|  
|relative_file_path|**nvarchar(256)**|Caminho para os dados ou arquivo delta, relativo ao local do contêiner.|  
|file_type|**tinyint**|0 para arquivo de dados.<br /><br /> 1 para arquivo delta.<br /><br /> NULL se a coluna de estado estiver definida como 7.|  
|file_type_desc|**nvarchar (60)**|O tipo de arquivo: DATA_FILE, DELTA_FILE ou NULL se a coluna de estado for definida como 7.|  
|internal_storage_slot|**int**|O índice do arquivo na matriz de armazenamento interna. NULL se a coluna de estado não estiver definida como 2 ou 3.|  
|checkpoint_pair_file_id|**uniqueidentifier**|Os dados ou arquivo delta correspondentes.|  
|file_size_in_bytes|**bigint**|Tamanho do arquivo usado. NULL se a coluna de estado estiver definida como 5, 6 ou 7.|  
|file_size_used_in_bytes|**bigint**|Tamanho utilizado do arquivo que está sendo usado NULL se a coluna de estado estiver definida como 5, 6 ou 7.<br /><br /> Para os pares de arquivos de ponto de verificação que ainda estão sendo populados, essa coluna será atualizada após o próximo ponto de verificação.|  
|inserted_row_count|**bigint**|Número de linhas no arquivo de dados.|  
|deleted_row_count|**bigint**|Número de linhas excluídas no arquivo delta.|  
|drop_table_deleted_row_count|**bigint**|O número de linhas nos arquivos de dados afetados por uma tabela. Aplica-se aos arquivos de dados quando o estado da coluna for igual a 1.<br /><br /> Mostra as contagens de linhas excluídas das tabelas removidas. As estatísticas drop_table_deleted_row_count são compiladas depois que a coleta de lixo de memória das linhas nas tabelas removidas é concluída e um ponto de verificação é realizado. Se você reiniciar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] antes que as estatísticas de tabelas removidas apareçam nessa coluna, as estatísticas serão atualizadas como parte da recuperação. O processo de recuperação não carrega linhas das tabelas removidas. As estatísticas das tabelas removidas são compiladas durante a fase de carregamento e relatadas nessa coluna quando a recuperação é concluída.|  
|state|**int**|0-CRIADO<br /><br /> 1-EM CONSTRUÇÃO<br /><br /> 2 - ATIVO<br /><br /> 3-DESTINO DE MESCLAGEM<br /><br /> 4-FONTE MESCLADA<br /><br /> 5-NECESSÁRIO PARA BACKUP/HA<br /><br /> 6-EM TRANSIÇÃO PARA MARCA PARA EXCLUSÃO<br /><br /> 7-MARCAS PARA EXCLUSÃO|  
|state_desc|**nvarchar (60)**|Pré-criado-um pequeno conjunto de pares de arquivos de dados e Delta, também conhecido como CFPs (pares de arquivos de ponto de verificação), é mantido pré-alocado para minimizar ou eliminar as esperas para alocar novos arquivos à medida que as transações são executadas. Eles são totalmente utilizados com um tamanho de arquivo de dados de 128 MB e tamanho de arquivo delta de 8 MB, mas não contêm dados. O número de CFPs é calculado como o número de processadores lógicos ou de agendadores (um por núcleo, sem número máximo) com um mínimo de 8. Essa é uma sobrecarga de armazenamento fixa em bancos de dados com tabelas com otimização de memória.<br /><br /> EM construção-conjunto de CFPs que armazena linhas de dados recentemente inseridas e possivelmente excluídas desde o último ponto de verificação.<br /><br /> ATIVO - Esses contêm as linhas inseridas e excluídas dos pontos de verificação fechados anteriores. Esses CFPs contêm todas as linhas inseridas e excluídas necessárias antes da aplicação da parte ativa do log de transações na reinicialização do banco de dados. O tamanho dessas CFPs será aproximadamente 2 vezes o tamanho das tabelas com otimização de memória na memória, supondo que a operação de mesclagem esteja atualmente com a carga de trabalho transacional.<br /><br /> DESTINO de MESCLAgem – o CFP armazena as linhas de dados consolidadas das CFP que foram identificadas pela política de mesclagem. Assim que a mesclagem for instalada, a opção MESCLAR DESTINO entrará no estado ATIVO.<br /><br /> ORIGEM MESCLAda-depois que a operação de mesclagem for instalada, os CFPs de origem serão marcados como origem MESCLAda. Observe que, o avaliador de política de mesclagem pode identificar várias mesclagens, mas um CFP só pode participar de uma operação de mesclagem.<br /><br /> NECESSÁRIO para BACKUP/HA-depois que a mesclagem tiver sido instalada e o CFP de destino de MESCLAgem fizer parte do ponto de verificação durável, a fonte de mesclagem CFPs passará para esse estado. Os CFPs nesse estado são necessários para exatidão operacional do banco de dados da tabela com otimização de memória.  Por exemplo, restaurar de um ponto de verificação durável para voltar no tempo. Um CFP pode ser marcado para coleta de lixo depois que o ponto de truncamento do log passar de seu intervalo de transações.<br /><br /> EM transição para marca de exclusão-esses CFPs não são necessários pelo mecanismo OLTP na memória e podem ser coletados como lixo. Esse estado indica que esses CFPs estão aguardando o thread em segundo plano para fazer a transição deles para o próximo estado, que é MARCA DE EXCLUSÃO.<br /><br /> MARCA de exclusão-esses CFPs estão aguardando para serem coletados pelo lixo pelo coletor de lixo de FileStream. ([sp_filestream_force_garbage_collection &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/filestream-and-filetable-sp-filestream-force-garbage-collection.md))|  
|lower_bound_tsn|**bigint**|O limite inferior de transações contidas no arquivo. Nulo se a coluna de estado for diferente de 2, 3 ou 4.|  
|upper_bound_tsn|**bigint**|O limite superior de transações contidas no arquivo. Nulo se a coluna de estado for diferente de 2, 3 ou 4.|  
|last_backup_page_count|**int**|Contagem de página lógica que é determinada no último backup. Aplica-se quando a coluna de estado estiver definida como 2, 3, 4 ou 5. NULL se a contagem de páginas não for conhecida.|  
|delta_watermark_tsn|**int**|A transação do último ponto de verificação que gravou neste arquivo delta. Essa é a marca d'água do arquivo delta.|  
|last_checkpoint_recovery_lsn|**nvarchar (23)**|Número de sequência do log de recuperação do último ponto de verificação que ainda precisa do arquivo.|  
|tombstone_operation_lsn|**nvarchar (23)**|O arquivo será excluído uma vez que tombstone_operation_lsn ir para trás do número de sequência de log de truncamento do registro.|  
|logical_deletion_log_block_id|**bigint**|Aplica-se somente ao estado 5.|  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão `VIEW DATABASE STATE` no servidor.  
  
## <a name="use-cases"></a>Casos de uso  
 Você pode estimar o armazenamento usado pelo OLTP na memória da seguinte maneira:  
  
```  
-- total storage used by In-Memory OLTP  
SELECT SUM (file_size_in_bytes)/(1024*1024) as file_size_in_MB  
FROM sys.dm_db_xtp_checkpoint_files  
```  
  
  
Para ver uma análise da utilização de armazenamento por Estado e tipo de arquivo, execute a seguinte consulta:
  
```  
SELECT state_desc  
 , file_type_desc  
 , COUNT(*) AS [count]  
 , SUM(file_size_in_bytes) / 1024 / 1024 AS [on-disk size MB]   
FROM sys.dm_db_xtp_checkpoint_files  
GROUP BY state, state_desc, file_type, file_type_desc  
ORDER BY state, file_type  
```  
  

  
## <a name="see-also"></a>Consulte Também  
 [Exibições de gerenciamento dinâmico de tabela com otimização de memória &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
