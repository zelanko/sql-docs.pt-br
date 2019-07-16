---
title: sys.dm_database_replica_states (banco de dados SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_database_replica_states_TSQL
- sys.dm_database_replica_states
- dm_database_replica_states
- dm_database_replica_states_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- sys.dm_database_replica_states dynamic management view
author: stevestein
ms.author: sstein
ms.openlocfilehash: a927b31e12aaf01c5fe30bfcf530bd049989e48f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68005033"
---
# <a name="sysdmdatabasereplicastates-azure-sql-database"></a>sys.dm_database_replica_states (Banco de Dados SQL do Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Retorna uma linha para o banco de dados, expondo o estado da réplica local.  
  
> [!IMPORTANT]
> Dependendo da ação dos estados de nível mais alto, as informações de estado do banco de dados podem estar indisponíveis ou desatualizadas. Além disso, os valores têm relevância local apenas. 
   
|Nome da coluna|Tipo de dados|Descrição (sobre a réplica primária)|  
|-----------------|---------------|----------------------------------------|  
|**database_id**|**int**|Identificador do banco de dados.|  
|**group_id**|**uniqueidentifier**|O identificador do grupo de disponibilidade ao qual o banco de dados pertence.|  
|**replica_id**|**uniqueidentifier**|O identificador da réplica de disponibilidade dentro do grupo de disponibilidade.|  
|**group_database_id**|**uniqueidentifier**|O identificador do banco de dados dentro do grupo de disponibilidade. Esse identificador é idêntico em cada réplica à qual este banco de dados é unido.|  
|**is_local**|**bit**|Se o banco de dados de disponibilidade é local, um dos seguintes:<br /><br /> 0 = O banco de dados não é local para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> 1 = O banco de dados é local para a instância do servidor.|  
|**is_primary_replica**|**bit**|Retorna 1 se a réplica for primária, ou 0 se for uma réplica secundária.<br /><br />**Aplica-se a:** [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**synchronization_state**|**tinyint**|Estado da movimentação de dados, um dos valores a seguir.<br /><br /> 0 = não sincronizando. Para um banco de dados primário, indica que o banco de dados não está pronto para sincronizar seu log de transações com os bancos de dados secundários correspondentes. Para um banco de dados secundário, indica que o banco de dados não iniciou a sincronização de log devido a um problema de conexão, está sendo suspenso ou está passando por estados de transição durante a inicialização ou uma troca de função.<br /><br /> 1 = Synchronizing. Para um banco de dados primário, indica que o banco de dados está pronto para aceitar uma solicitação de exame de um banco de dados secundário. Para um banco de dados secundário, indica que o movimento de dados ativo está ocorrendo para o banco de dados.<br /><br /> 2 = Synchronized. Um banco de dados primário mostra SYNCHRONIZED em vez de SYNCHRONIZING. Um banco de dados secundário de confirmação síncrona mostrará sincronizado quando o cache local informar que o banco de dados está pronto para failover e quando está sincronizando.<br /><br /> 3 = revertendo. Indica a fase do processo de desfazer em que um banco de dados secundário está obtendo páginas ativamente do banco de dados primário.<br />**Cuidado:** Quando um banco de dados em uma réplica secundária estiver no estado REVERTING, forçar failover na réplica secundária deixa o banco de dados em um estado no qual ele não pode ser iniciado como um banco de dados primário. O banco de dados precisará ser reconectado como um banco de dados secundário ou você precisará aplicar novos registros de log de um backup de log.<br /><br /> 4 = inicializando. Indica a fase de desfazer em que o log de transações que exigiu que um banco de dados secundário ficasse em dia com o LSN de desfazer está sendo enviado e protegido em uma réplica secundária.<br />**Cuidado:** Quando um banco de dados em uma réplica secundária estiver no estado INITIALIZING, forçar failover na réplica secundária deixa o banco de dados em um estado no qual ele não pode ser iniciado como um banco de dados primário. O banco de dados precisará ser reconectado como um banco de dados secundário ou você precisará aplicar novos registros de log de um backup de log.|  
|**synchronization_state_desc**|**nvarchar(60)**|Descrição do estado da movimentação de dados, um dos seguintes:<br /><br /> NOT SYNCHRONIZING<br /><br /> SYNCHRONIZING<br /><br /> SYNCHRONIZED<br /><br /> REVERTING<br /><br /> INITIALIZING|  
|**is_commit_participant**|**bit**|0 = A confirmação da transação não está sincronizada em relação a este banco de dados.<br /><br /> 1 = A confirmação da transação está sincronizada em relação a este banco de dados.<br /><br /> Para um banco de dados em uma réplica de disponibilidade de confirmação assíncrona, este valor é sempre 0.<br /><br /> Para um banco de dados em uma réplica de disponibilidade de confirmação síncrona, este valor é preciso somente no banco de dados primário.|  
|**synchronization_health**|**tinyint**|Reflete a interseção do estado de sincronização de um banco de dados que está associado ao grupo de disponibilidade na réplica de disponibilidade e o modo de disponibilidade da réplica de disponibilidade (confirmação síncrona ou assíncrona modo de confirmação), uma da valores a seguir.<br /><br /> 0 = não íntegro. O **synchronization_state** do banco de dados é 0 (NOT SYNCHRONIZING).<br /><br /> 1 = parcialmente íntegro. Um banco de dados em uma réplica de disponibilidade de confirmação síncrona será considerado parcialmente Íntegro se **synchronization_state** for 1 (SYNCHRONIZING).<br /><br /> 2 = íntegro. Um banco de dados em uma réplica de disponibilidade de confirmação síncrona será considerado Íntegro se **synchronization_state** é 2 (SYNCHRONIZED), e um banco de dados em uma réplica de disponibilidade de confirmação assíncrona será considerado Íntegro se **synchronization_state** for 1 (SYNCHRONIZING).|  
|**synchronization_health_desc**|**nvarchar(60)**|Descrição do **synchronization_health** do banco de dados de disponibilidade.<br /><br /> NOT_HEALTHY<br /><br /> PARTIALLY_HEALTHY<br /><br /> HEALTHY|  
|**database_state**|**tinyint**|0 = Online<br /><br /> 1 = Restaurando<br /><br /> 2 = Recuperando<br /><br /> 3 = Recuperação pendente<br /><br /> 4 = Suspeito<br /><br /> 5 = Emergência<br /><br /> 6 = Offline<br /><br /> **Observação:** Mesmo que **estado** coluna em sys. Databases.|  
|**database_state_desc**|**nvarchar(60)**|Descrição do **database_state** da réplica de disponibilidade.<br /><br /> ONLINE<br /><br /> RESTORING<br /><br /> RECOVERING<br /><br /> RECOVERY_PENDING<br /><br /> SUSPECT<br /><br /> EMERGENCY<br /><br /> OFFLINE<br /><br /> **Observação:** Mesmo que **state_desc** coluna em sys. Databases.|  
|**is_suspended**|**bit**|Estado do banco de dados, um dos seguintes:<br /><br /> 0 - Retomado<br /><br /> 1 = Suspenso|  
|**suspend_reason**|**tinyint**|Se o banco de dados estiver suspenso, o motivo do estado de suspensão, um dos seguintes:<br /><br /> 0 = Ação do usuário<br /><br /> 1 = Suspensão do parceiro<br /><br /> 2 = Refazer<br /><br /> 3 = Capturar<br /><br /> 4 = Aplicar<br /><br /> 5 = Reiniciar<br /><br /> 6 = Desfazer<br /><br /> 7 = Revalidação<br /><br /> 8 = Erro no cálculo do ponto de sincronização da réplica secundária|  
|**suspend_reason_desc**|**nvarchar(60)**|Descrição do motivo do estado da suspensão do banco de dados, um dos seguintes:<br /><br /> SUSPEND_FROM_USER = Uma movimentação de dados suspensa manualmente pelo usuário<br /><br /> SUSPEND_FROM_PARTNER = A réplica do banco de dados é suspensa após um failover forçado<br /><br /> SUSPEND_FROM_REDO = Ocorreu um erro durante a fase refazer<br /><br /> SUSPEND_FROM_APPLY = Ocorreu um erro durante a gravação do log no arquivo (consulte o log de erros)<br /><br /> SUSPEND_FROM_CAPTURE = Ocorreu um erro durante a captura do log na réplica primária<br /><br /> SUSPEND_FROM_RESTART = A réplica do banco de dados foi suspensa antes da reinicialização do banco de dados (consulte o log de erros)<br /><br /> SUSPEND_FROM_UNDO = Ocorreu um erro durante a fase desfazer (consulte o log de erros)<br /><br /> SUSPEND_FROM_REVALIDATION = Incompatibilidade de alteração de log detectada na reconexão (consulte o log de erros)<br /><br /> SUSPEND_FROM_XRF_UPDATE = Não é possível localizar o ponto de log comum (consulte o log de erros)|  
|**recovery_lsn**|**numeric(25,0)**|Na réplica primária, o final do log de transações antes de o banco de dados primário gravar outro novo registro de log depois da recuperação ou do failover. Para um determinado banco de dados secundário, se este valor for menor que o LSN protegido atual (last_hardened_lsn), recovery_lsn será o valor para o qual este banco de dados secundário precisaria ressincronizar (ou seja, reverter e reinicializar). Se este valor for maior que ou igual ao LSN protegido atual, a ressincronização será desnecessária e não ocorrerá.<br /><br /> **recovery_lsn** reflete uma ID de bloco de log preenchida com zeros. Não é um LSN (número de sequência de log) real.|  
|**truncation_lsn**|**numeric(25,0)**|Na réplica primária, para o banco de dados primário, reflete o LSN de truncamento de log mínimo em todos os bancos de dados secundários correspondentes. Se o truncamento de log local estiver bloqueado (como por uma operação de backup), esse LSN poderá ser mais alto que o LSN de truncamento local.<br /><br /> Para um determinado banco de dados secundário, reflete o ponto de truncamento desse banco de dados.<br /><br /> **truncation_lsn** reflete uma ID de bloco de log preenchida com zeros. Não é um número de sequência de log real.|  
|**last_sent_lsn**|**numeric(25,0)**|O identificador do bloco de log que indica o ponto até o qual todos os blocos de log foram enviados pela primária. Esta é a ID do próximo bloco de log que será enviado, em vez da ID do bloco de log enviado mais recentemente.<br /><br /> **last_sent_lsn** reflete uma ID de bloco de log preenchida com zeros, não é um número de sequência de log real.|  
|**last_sent_time**|**datetime**|A hora em que o último bloco de log foi enviado.|  
|**last_received_lsn**|**numeric(25,0)**|Id de bloco de log que identifica o ponto até o qual todos os blocos de log foram recebidos pela réplica secundária que hospeda este banco de dados secundário.<br /><br /> **last_received_lsn** reflete uma ID de bloco de log preenchida com zeros. Não é um número de sequência de log real.|  
|**last_received_time**|**datetime**|A hora em que a ID do bloco de log na última mensagem recebida foi lido na réplica secundária.|  
|**last_hardened_lsn**|**numeric(25,0)**|Início do Bloco de Log que contém os registros de log do último LSN de proteção em um banco de dados secundário.<br /><br /> Em um banco de dados primário de confirmação assíncrona ou em um banco de dados de confirmação síncrona cuja política atual é "atraso", o valor é o NULL. Para bancos de dados primários outros confirmação síncrona, **last_hardened_lsn** indica o mínimo do LSN de proteção em todos os bancos de dados secundários.<br /><br /> **Observação: last_hardened_lsn** reflete uma ID de bloco de log preenchida com zeros. Não é um número de sequência de log real.|  
|**last_hardened_time**|**datetime**|Em um banco de dados secundário, hora do identificador do bloco de log para o último LSN protegido (**last_hardened_lsn**). Em um banco de dados primário, reflete a hora que corresponde ao LSN de proteção mínimo.|  
|**last_redone_lsn**|**numeric(25,0)**|O número de sequência de log real do último registro de log que foi desfeito no banco de dados secundário. **last_redone_lsn** é sempre menor que **last_hardened_lsn**.|  
|**last_redone_time**|**datetime**|A hora em que o último registro de log foi refeito no banco de dados secundário.|  
|**log_send_queue_size**|**bigint**|Quantidade de registros de log do banco de dados primário que não foram enviados aos bancos de dados secundários, em KB (kilobytes).|  
|**log_send_rate**|**bigint**|Taxa na qual os dados enviado de instância réplica primária média durante o último período ativo, em quilobytes (KB) por segundo.|  
|**redo_queue_size**|**bigint**|A quantidade de registros de log nos arquivos de log da réplica secundária que ainda não foram refeitos, em KB.|  
|**redo_rate**|**bigint**|Média taxa na qual os registros de log estão sendo refeitos em um determinado banco de dados secundário, em quilobytes (KB) / segundo.|  
|**filestream_send_rate**|**bigint**|A taxa na qual os arquivos FILESTREAM são enviados à réplica secundária, em KB/segundo.|  
|**end_of_log_lsn**|**numeric(25,0)**|O fim do log do LSN local. O LSN real que corresponde ao último registro de log no cache de log nos bancos de dados primário e secundário. Na réplica primária, as linhas secundárias refletem o fim do log do LSN das mensagens de progresso mais recentes que as réplicas secundárias enviaram à réplica primária.<br /><br /> **end_of_log_lsn** reflete uma ID de bloco de log preenchida com zeros. Não é um número de sequência de log real.|  
|**last_commit_lsn**|**Numeric(25,0)**|O número de sequência de log real que corresponde ao último registro de confirmação no log de transações.<br /><br /> No banco de dados primário, corresponde ao último registro de confirmação processado. As linhas para bancos de dados secundários mostram o número de sequência de log que a réplica secundária enviou para a primária.<br /><br /> Na réplica secundária, é o último registro de confirmação refeito.|  
|**last_commit_time**|**datetime**|A hora correspondente ao último registro de confirmação.<br /><br /> No banco de dados secundário, essa hora é a mesma do banco de dados primário.<br /><br /> Na réplica primária, cada linha de banco de dados secundário exibe a hora em que a réplica secundária que hospeda aquele banco de dados secundário relatou de volta para a réplica primária. A diferença de tempo entre as linhas de banco de dados primário e um determinado banco de dados secundário representa aproximadamente o ponto de objetivo de recuperação (RPO), supondo que o processo de refazer é alcançado e que o progresso foi relatado de volta para a réplica primária pela réplica secundária.|  
|**low_water_mark_for_ghosts**|**bigint**|Um número aumentado de maneira constante para o banco de dados, que indica uma marca d'água inferior usada pela limpeza de fantasma no banco de dados primário. Se esse número não estiver aumentando ao longo do tempo, isso indicará que a limpeza fantasma talvez não esteja ocorrendo. Para decidir quais linhas fantasmas devem ser limpas, a réplica primária usa o valor mínimo dessa coluna para este banco de dados em todas as réplicas de disponibilidade (inclusive a réplica primária).|  
|**secondary_lag_seconds**|**bigint**|O número de segundos que a réplica secundária está atrás da réplica primária durante a sincronização.<br /><br />**Aplica-se a:** [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|**quorum_commit_lsn**|**Numeric(25,0)**|Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.|
|**quorum_commit_time**|**datetime**|Identificado apenas para fins informativos. Sem suporte. A compatibilidade futura não está garantida.|


## <a name="permissions"></a>Permissões

, é necessário ter permissão VIEW SERVER STATE no servidor.  


## <a name="see-also"></a>Consulte também

- [Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)
- [Monitorar grupos de disponibilidade &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)