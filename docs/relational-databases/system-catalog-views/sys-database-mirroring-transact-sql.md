---
title: sys. database_mirroring (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.database_mirroring
- database_mirroring
- sys.database_mirroring_TSQL
- database_mirroring_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.database_mirroring catalog view
ms.assetid: 480de2b0-2c16-497d-a6a3-bf7f52a7c9a0
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 515f3dad1f07535a5d0c8e590adadce0923180db
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68022753"
---
# <a name="sysdatabasemirroring-transact-sql"></a>sys.database_mirroring (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém uma linha para cada banco de dados na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se o banco de dados não está ONLINE ou o espelhamento de banco de dados não estiver habilitado, os valores de todas as colunas exceto database_id será NULL.  
  
 Para ver a linha para um banco de dados que não seja mestre ou tempdb, você deve ser o proprietário do banco de dados ou ter pelo menos permissão de nível de servidor ALTER ANY DATABASE ou VIEW ANY DATABASE ou permissão CREATE DATABASE no banco de dados mestre. Para ver os valores não nulos em um banco de dados espelho, você deve ser um membro do **sysadmin** função de servidor fixa.  
  
> [!NOTE]  
>  Se um banco de dados não participar no espelhamento, todas as colunas prefixadas com "mirroring_" serão NULL.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|ID do banco de dados. É exclusiva em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**mirroring_guid**|**uniqueidentifier**|ID da parceria de espelhamento.<br /><br /> NULL = banco de dados está inacessível ou não está espelhado.<br /><br /> Observação: Se o banco de dados não participar no espelhamento, todas as colunas prefixadas com "Mirroring _" serão NULL.|  
|**mirroring_state**|**tinyint**|Estado do banco de dados de espelhamento e da sessão de espelhamento de banco de dados.<br /><br /> 0 = Suspended<br /><br /> 1 = Desconectado do outro parceiro<br /><br /> 2 = Sincronização<br /><br /> 3 = Failover pendente<br /><br /> 4 = Sincronizado<br /><br /> 5 = Os parceiros não estão sincronizados. Failover impossível no momento.<br /><br /> 6 = Os parceiros estão sincronizados. Failover é potencialmente possível. Para obter informações sobre os requisitos para failover, consulte [Database Mirroring Operating Modes](../../database-engine/database-mirroring/database-mirroring-operating-modes.md).<br /><br /> NULL = O banco de dados está inacessível ou não está espelhado.|  
|**mirroring_state_desc**|**nvarchar(60)**|Descrição do estado do banco de dados de espelhamento e da sessão de espelhamento de banco de dados, pode ser um dentre:<br /><br /> DISCONNECTED<br /><br /> SYNCHRONIZED<br /><br /> SYNCHRONIZING<br /><br /> PENDING_FAILOVER<br /><br /> SUSPENDED<br /><br /> UNSYNCHRONIZED<br /><br /> SYNCHRONIZED<br /><br /> NULL<br /><br /> Para obter mais informações, veja [Estados de espelhamento &#40;SQL Server&#41;](../../database-engine/database-mirroring/mirroring-states-sql-server.md).|  
|**mirroring_role**|**tinyint**|Função atual do banco de dados local é reproduzida na sessão de espelhamento de banco de dados.<br /><br /> 1 = Principal<br /><br /> 2 = Espelhamento<br /><br /> NULL = O banco de dados está inacessível ou não está espelhado.|  
|**mirroring_role_desc**|**nvarchar(60)**|Descrição da função que o banco de dados local reproduz no espelhamento, pode ser uma dentre:<br /><br /> PRINCIPAL<br /><br /> MIRROR|  
|**mirroring_role_sequence**|**int**|O número de horas que os parceiros de espelhamento alternaram as funções principal e de espelhamento devido a failover ou serviço forçado.<br /><br /> NULL = O banco de dados está inacessível ou não está espelhado.|  
|**mirroring_safety_level**|**tinyint**|A configuração de segurança para atualizações no banco de dados espelho:<br /><br /> 0 = Estado desconhecido<br /><br /> 1 = Desativado [assíncrono]<br /><br /> 2 = Completo [síncrono]<br /><br /> NULL = O banco de dados está inacessível ou não está espelhado.|  
|**mirroring_safety_level_desc**|**nvarchar(60)**|Configuração de segurança de transações para as atualizações no banco de dados espelho, pode ser uma dentre:<br /><br /> UNKNOWN<br /><br /> OFF<br /><br /> FULL<br /><br /> NULL|  
|**mirroring_safety_sequence**|**int**|Atualiza o número de sequência para alterações no nível de segurança de transações.<br /><br /> NULL = O banco de dados está inacessível ou não está espelhado.|  
|**mirroring_partner_name**|**nvarchar(128)**|Nome do servidor do parceiro de espelhamento de banco de dados.<br /><br /> NULL = O banco de dados está inacessível ou não está espelhado.|  
|**mirroring_partner_instance**|**nvarchar(128)**|O nome de instância e nome do computador de outro parceiro. Os clientes precisarão destas informações para se conectar ao parceiro se ele se tornar o servidor principal.<br /><br /> NULL = O banco de dados está inacessível ou não está espelhado.|  
|**mirroring_witness_name**|**nvarchar(128)**|Nome do servidor da testemunha de espelhamento do banco de dados.<br /><br /> NULL = Não há testemunha.|  
|mirroring_witness_state|**tinyint**|Estado da testemunha na sessão de espelhamento de banco de dados no banco de dados, pode ser um dentre:<br /><br /> 0 = Desconhecido<br /><br /> 1 = conectado<br /><br /> 2 = Desconectado<br /><br /> NULL = Não há testemunha, o banco de dados não está online ou o banco de dados não é espelhado.|  
|**mirroring_witness_state_desc**|**nvarchar(60)**|Descrição de estado, pode ser uma dentre:<br /><br /> UNKNOWN<br /><br /> CONNECTED<br /><br /> DISCONNECTED<br /><br /> NULL|  
|**mirroring_failover_lsn**|**numeric(25,0)**|LSN (número de sequência de log) do registro de log de transação mais recente, que tem garantia de ser intensificado em disco em ambos os parceiros. Após um failover, o **mirroring_failover_lsn** é usado pelos parceiros como o ponto de reconciliação, no qual o novo servidor espelho começa a sincronizar o novo banco de dados espelho com o novo banco de dados principal.|  
|**mirroring_connection_timeout**|**int**|Tempo limite de conexão do espelhamento em segundos. Esse é o número de segundos de espera para um resposta de um parceiro ou testemunha antes de considerá-los indisponíveis. O valor do tempo limite padrão é de 10 segundos.<br /><br /> NULL = O banco de dados está inacessível ou não está espelhado.|  
|**mirroring_redo_queue**|**int**|Quantidade máxima de log a ser refeito no espelho. Se mirroring_redo_queue_type for definido como UNLIMITED, que é a configuração padrão, essa coluna é NULL. Se o banco de dados não estiver online, essa coluna também será NULL.<br /><br /> Caso contrário, essa coluna contém a quantidade máxima de log em megabytes. Quando o máximo for atingido, o log será temporariamente paralisado no principal à medida que o servidor espelho for atualizado. Esse recurso limita o tempo de failover.<br /><br /> Para obter mais informações, veja [Estime a interrupção do serviço durante troca de função &#40;Espelhamento de Banco de Dados&#41;](../../database-engine/database-mirroring/estimate-the-interruption-of-service-during-role-switching-database-mirroring.md).|  
|**mirroring_redo_queue_type**|**nvarchar(60)**|UNLIMITED indica que o espelhamento não inibirá a fila para ser refeito. Essa é a configuração padrão.<br /><br /> MB para tamanho máximo da fila a refazer em megabytes. Observe que se o tamanho da fila tiver sido especificado como kilobytes ou gigabytes, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] converterá o valor em megabytes.<br /><br /> Se o banco de dados não estiver online, essa coluna será NULL.|  
|**mirroring_end_of_log_lsn**|**numeric(25,0)**|O fim do log local que foi liberado para o disco. Isso é equivalente ao LSN intensificado do servidor espelho (consulte a **mirroring_failover_lsn** coluna).|  
|**mirroring_replication_lsn**|**numeric(25,0)**|O LSN máximo que a replicação pode enviar.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [sys.database_mirroring_witnesses &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)   
 [sys.database_mirroring_endpoints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql.md)   
 [Exibição de catálogo do bancos de dados e de arquivos &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql.md)   
 [Consultando as perguntas frequentes do catálogo do sistema do SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
