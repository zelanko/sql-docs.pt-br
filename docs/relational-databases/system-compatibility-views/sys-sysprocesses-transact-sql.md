---
title: sys. sysprocesses (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysprocesses_TSQL
- sys.sysprocesses_TSQL
- sys.sysprocesses
- sysprocesses
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sysprocesses compatibility view
- sysprocesses system table
ms.assetid: 60a36d36-54b3-4bd6-9cac-702205a21b16
author: rothja
ms.author: jroth
ms.openlocfilehash: 6aa40d6a7363dd991dc37ed5c619b656e74f0eed
ms.sourcegitcommit: 86268d297e049adf454b97858926d8237d97ebe2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78866364"
---
# <a name="syssysprocesses-transact-sql"></a>sys.sysprocesses (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém informações sobre os processos que estão em execução em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Eles podem ser processos do cliente ou processos do sistema. Para acessar sysprocesses, você deve estar no contexto do banco de dados mestre ou deve usar o nome de três partes master.dbo.sysprocesses.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|spid|**smallint**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ID da sessão.|  
|kpid|**smallint**|ID do thread do Windows.|  
|blocked|**smallint**|ID da sessão que está bloqueando a solicitação. Se esta coluna for NULL, a solicitação não estará bloqueada ou as informações da sessão de bloqueio não estarão disponíveis (ou não podem ser identificadas).<br /><br /> -2 = O recurso de bloqueio pertence a uma transação distribuída órfã.<br /><br /> -3 = O recurso de bloqueio pertence a uma transação de recuperação adiada.<br /><br /> -4 = A ID da sessão do proprietário da trava de bloqueio não pôde ser determinada devido a transições internas de estado da trava.|  
|waittype|**binário (2)**|Reservado.|  
|waittime|**bigint**|Tempo de espera atual em milissegundos.<br /><br /> 0 = O processo não está esperando.|  
|lastwaittype|**nchar (32)**|Uma cadeia de caracteres que indica o nome do tipo de espera último ou atual.|  
|waitresource|**nchar (256)**|Representação textual de um recurso de bloqueio.|  
|dbid|**smallint**|ID do banco de dados usado atualmente pelo processo.|  
|uid|**smallint**|ID do usuário que executou o comando. Excederá ou retornará NULL se o número de usuários e funções exceder 32.767.|  
|cpu|**int**|Tempo de CPU cumulativo para o processo. A entrada é atualizada para todos os processos, independentemente da opção SET STATISTICS TIME ser ON ou OFF.|  
|physical_io|**bigint**|Leituras e gravações de disco cumulativas para o processo.|  
|memusage|**int**|Número de páginas no cache de procedimento que estão atualmente alocadas para este processo. Um número negativo indica que o processo está liberando a memória alocada por outro processo.|  
|login_time|**datetime**|Hora na qual um processo de cliente efetuou logon no servidor.|  
|last_batch|**datetime**|Última vez que um processo de cliente executou uma chamada de procedimento armazenado remoto ou uma instrução EXECUTE.|  
|ecid|**smallint**|ID do contexto de execução usado para identificar exclusivamente os subthreads que operam em nome de um único processo.|  
|open_tran|**smallint**|Número de transações abertas para o processo.|  
|status|**nchar (30)**|Status do ID do processo. Os valores possíveis são:<br /><br /> **inativo** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está redefinindo a sessão. = <br /><br /> **running** = a sessão está executando um ou mais lotes. Quando são habilitados MARS (Vários Conjuntos de Resultados Ativos), uma sessão pode executar vários lotes. Para obter mais informações, confira [Usando o MARS &#40;conjunto de resultados ativos múltiplos&#41;](../../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md).<br /><br /> **background** = a sessão está executando uma tarefa em segundo plano, como detecção de deadlock.<br /><br /> **Rollback** = a sessão tem uma reversão de transação em andamento.<br /><br /> **pendente** = a sessão está aguardando que um thread de trabalho fique disponível.<br /><br /> **executável** = a tarefa na sessão está na fila executável de um Agendador enquanto aguarda para obter uma Quantum de tempo.<br /><br /> **Spinloop** = a tarefa na sessão está aguardando que um spinlock fique livre.<br /><br /> **suspenso** = a sessão está aguardando que um evento, como e/s, seja concluído.|  
|sid|**binário (86)**|GUID (Identificador Global Exclusivo) do usuário.|  
|hostname|**nchar (128)**|Nome da estação de trabalho.|  
|program_name|**nchar (128)**|Nome do programa aplicativo.|  
|hostprocess|**nchar (10)**|Número de ID do processo da estação de trabalho.|  
|cmd|**nchar (52)**|Comando sendo executado atualmente.|  
|nt_domain|**nchar (128)**|Domínio do Windows do cliente, se estiver usando Autenticação do Windows, ou uma conexão confiável.|  
|nt_username|**nchar (128)**|Nome de usuário do Windows para o processo, se estiver usando Autenticação do Windows, ou uma conexão confiável.|  
|net_address|**nchar (12)**|Identificador exclusivo atribuído para o adaptador de rede na estação de trabalho de cada usuário. Quando um usuário fizer o logon, este identificador será inserido na coluna net_address.|  
|net_library|**nchar (12)**|Coluna na qual a biblioteca de rede do cliente é armazenada. Todo processo de cliente entra em uma conexão de rede. As conexões de rede têm uma biblioteca de rede associada a elas que as permite estabelecer a conexão.|  
|loginame|**nchar (128)**|Nome de logon.|  
|context_info|**binário (128)**|Dados armazenados em um lote usando a instrução SET CONTEXT_INFO.|  
|sql_handle|**binário (20)**|Representa o lote ou o objeto atualmente em execução.<br /><br /> **Observação** Esse valor é derivado do endereço de lote ou de memória do objeto. Esse valor não é calculado usando o algoritmo com base em hash do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|stmt_start|**int**|Deslocamento inicial da instrução SQL atual para o sql_handle especificado.|  
|stmt_end|**int**|Deslocamento final da instrução SQL atual para o sql_handle especificado.<br /><br /> -1 = A instrução atual é executada até o final dos resultados retornados pela função fn_get_sql do sql_handle especificado.|  
|request_id|**int**|ID da solicitação. Usado para identificar solicitações em execução em uma sessão específica.|
|page_resource |**binário (8)** |**Aplica-se ao**: [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] <br /><br /> Uma representação hexadecimal de 8 bytes do recurso de página se a `waitresource` coluna contiver uma página. |  
  
## <a name="remarks"></a>Comentários  
 Se um usuário tiver permissão VIEW SERVER STATE no servidor, ele verá todas as sessões em execução na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; caso contrário, verá apenas a sessão atual.  
  
## <a name="see-also"></a>Consulte Também  
 [Funções e exibições de gerenciamento dinâmico relacionadas à execução &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [Mapeando tabelas do sistema para exibições do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Exibições de compatibilidade &#40;&#41;Transact-SQL](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
