---
title: sp_who (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_who_TSQL
- sp_who
dev_langs:
- TSQL
helpviewer_keywords:
- sp_who
ms.assetid: 132dfb08-fa79-422e-97d4-b2c4579c6ac5
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: bfcf04c0f6dd7455bac9beaa65b29eb1b2a8f9cc
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85891210"
---
# <a name="sp_who-transact-sql"></a>sp_who (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Fornece informações sobre usuários, sessões e processos atuais em uma instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] . As informações podem ser filtradas para retornar somente os processos que não estão ociosos, que pertencem a um usuário específico ou que pertencem a uma sessão específica.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_who [ [ @loginame = ] 'login' | session ID | 'ACTIVE' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @loginame = ] 'login' | session ID | 'ACTIVE'`É usado para filtrar o conjunto de resultados.  
  
 o *logon* é **sysname** que identifica os processos que pertencem a um logon específico.  
  
 *ID de sessão* é um número de identificação de sessão que pertence à [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância. a *ID da sessão* é **smallint**.  
  
 **Ativo** exclui sessões que estão aguardando o próximo comando do usuário.  
  
 Se nenhum valor for fornecido, o procedimento relatará todas as sessões que pertencem à instância.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 **sp_who** retorna um conjunto de resultados com as informações a seguir.  
  
|Coluna|Tipo de dados|Descrição|  
|------------|---------------|-----------------|  
|**SPID**|**smallint**|ID da sessão.|  
|**ecid**|**smallint**|ID do contexto de execução de determinado thread associado a uma ID de sessão específica.<br /><br /> ECID = {0, 1, 2, 3,... *n*}, em que 0 sempre representa o thread principal ou pai, e {1, 2, 3,... *n*} representa os subsegmentos.|  
|**status**|**nchar(30)**|Status do processo. Os valores possíveis são:<br /><br /> **inativo**. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está reiniciando a sessão.<br /><br /> **em execução**. A sessão está executando um ou mais lotes. Quando são habilitados MARS (Vários Conjuntos de Resultados Ativos), uma sessão pode executar vários lotes. Para obter mais informações, consulte [usando vários conjuntos de resultados ativos &#40;MARS&#41;](../../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md).<br /><br /> **plano de fundo**. A sessão está executando uma tarefa em segundo plano, como detecção de deadlock.<br /><br /> **reversão**. A sessão tem uma reversão de transação em processo.<br /><br /> **pendente**. A sessão está aguardando que um thread de trabalho seja disponibilizado.<br /><br /> **executável**. A tarefa da sessão está na fila executável de um agendador enquanto aguarda para obter um quantum de hora.<br /><br /> **spinloop**. A tarefa da sessão está aguardando que um spinlock seja liberado.<br /><br /> **suspenso**. A sessão está aguardando que um evento, como E/S, seja concluído.|  
|**loginame**|**nchar(128)**|Nome de logon associado a determinado processo.|  
|**hostname**|**nchar(128)**|Nome do host ou computador de cada processo.|  
|**blk**|**Char (5)**|ID de sessão do processo de bloqueio, se houver. Caso contrário, essa coluna será zero.<br /><br /> Quando uma transação associada a uma ID de sessão especificada for bloqueada por uma transação distribuída órfã, essa coluna retornará um '-2' para o bloqueio da transação órfã.|  
|**NomeDoBancoDeDados**|**nchar(128)**|Banco de dados usado pelo processo.|  
|**cmd**|**nchar(16)**|Comando [!INCLUDE[ssDE](../../includes/ssde-md.md)] (instrução [!INCLUDE[tsql](../../includes/tsql-md.md)], processo [!INCLUDE[ssDE](../../includes/ssde-md.md)] interno e assim por diante) sendo executado para o processo. No SQL Server 2019, o tipo de dados foi alterado para **nchar (26)**.|  
|**request_id**|**int**|ID de solicitações em execução em uma sessão específica.|  
  
 No caso de processamento paralelo, são criados subthreads para a ID de sessão específica. O thread principal é indicado como `spid = <xxx>` e `ecid =0`. Os outros subthreads têm o mesmo `spid = <xxx>` , mas com **ECID** > 0.  
  
## <a name="remarks"></a>Comentários  
 Um processo de bloqueio, que pode ter um bloqueio exclusivo, é um que está retendo recursos que outro processo precisa.  
  
 Todas as transações distribuídas órfãs recebem o valor de ID da sessão de '-2'. As transações distribuídas órfãs são transações distribuídas que não estão associadas a qualquer ID de sessão. Para obter mais informações, veja [Usar transações marcadas para recuperar bancos de dados relacionados de forma consistente &#40;Modelo de recuperação completa&#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md).  
  
 Consulte a coluna **is_user_process** de sys. dm_exec_sessions para separar os processos do sistema dos processos do usuário.  
  
## <a name="permissions"></a>Permissões  
 Requer permissão VIEW SERVER STATE no servidor para visualizar todas as sessões em execução na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Caso contrário, o usuário verá somente a sessão atual.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-listing-all-current-processes"></a>a. Relacionando todos os processos atuais  
 O exemplo a seguir usa `sp_who` sem parâmetros para relatar todos os usuários atuais.  
  
```  
USE master;  
GO  
EXEC sp_who;  
GO  
```  
  
### <a name="b-listing-a-specific-users-process"></a>B. Relacionando um processo de um usuário específico  
 O exemplo a seguir mostra como exibir informações sobre um único usuário atual através do nome de logon.  
  
```  
USE master;  
GO  
EXEC sp_who 'janetl';  
GO  
```  
  
### <a name="c-displaying-all-active-processes"></a>C. Exibindo todos os processos ativos  
  
```  
USE master;  
GO  
EXEC sp_who 'active';  
GO  
```  
  
### <a name="d-displaying-a-specific-process-identified-by-a-session-id"></a>D. Exibindo um processo específico identificado por uma ID de sessão  
  
```  
USE master;  
GO  
EXEC sp_who '10' --specifies the process_id;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_lock](../../relational-databases/system-stored-procedures/sp-lock-transact-sql.md)   
 [Processos desys.sys&#40;&#41;de Transact-SQL](../../relational-databases/system-compatibility-views/sys-sysprocesses-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
