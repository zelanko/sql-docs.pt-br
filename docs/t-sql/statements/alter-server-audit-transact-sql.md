---
description: ALTER SERVER AUDIT (Transact-SQL)
title: ALTER SERVER AUDIT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/07/2018
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_SERVER_AUDIT_TSQL
- ALTER SERVER AUDIT
dev_langs:
- TSQL
helpviewer_keywords:
- server audit [SQL Server]
- audits [SQL Server], specification
- ALTER SERVER AUDIT statement
ms.assetid: 63426d31-7a5c-4378-aa9e-afcf4f64ceb3
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||>=sql-server-linux-2017
ms.openlocfilehash: 0239db3ed1005d3238853ffd5f058174be823b4e
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97462197"
---
# <a name="alter-server-audit--transact-sql"></a>ALTER SERVER AUDIT (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  Altera um objeto de auditoria de servidor com o recurso [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Audit. Para obter mais informações, veja [Auditoria do SQL Server &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md).  

 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
ALTER SERVER AUDIT audit_name  
{  
    [ TO { { FILE ( <file_options> [, ...n] ) } | APPLICATION_LOG | SECURITY_LOG } | URL]  
    [ WITH ( <audit_options> [ , ...n] ) ]   
    [ WHERE <predicate_expression> ]  
}  
| REMOVE WHERE  
| MODIFY NAME = new_audit_name  
[ ; ]  
  
<file_options>::=  
{  
      FILEPATH = 'os_file_path'   
    | MAXSIZE = { max_size { MB | GB | TB } | UNLIMITED }   
    | MAX_ROLLOVER_FILES = { integer | UNLIMITED }   
    | MAX_FILES = integer   
    | RESERVE_DISK_SPACE = { ON | OFF }   
}  
  
<audit_options>::=  
{  
      QUEUE_DELAY = integer   
    | ON_FAILURE = { CONTINUE | SHUTDOWN | FAIL_OPERATION }   
    | STATE = = { ON | OFF }   
}  
  
<predicate_expression>::=  
{  
    [NOT ] <predicate_factor>   
    [ { AND | OR } [NOT ] { <predicate_factor> } ]   
    [,...n ]  
}  
  
<predicate_factor>::=   
    event_field_name { = | < > | ! = | > | > = | < | < = } { number | ' string ' }  
```  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 TO { FILE \| APPLICATION_LOG \| SECURITY \|URL}  
 Determina o local do destino da auditoria. As opções são um arquivo binário, o log de aplicativos do Windows ou o log de segurança do Windows.  

> [!IMPORTANT]
> Na Instância Gerenciada de SQL do Azure, a Auditoria do SQL funciona no nível de servidor e armazena arquivos `.xel` no Armazenamento de Blobs do Azure.
  
 FILEPATH **= '** _os\_file\_path_ **'**  
 O caminho da trilha de auditoria. O nome do arquivo é gerado com base no nome da auditoria e no GUID da auditoria.  
  
 MAXSIZE **=** _max\_size_  
 Especifica o tamanho máximo até o qual o arquivo de auditoria pode crescer. O valor de *max_size* deve ser um inteiro seguido de **MB**, **GB**, **TB** ou **UNLIMITED**. O tamanho mínimo que você pode especificar para *max_size* é 2 **MB** e o máximo é 2.147.483.647 **TB**. Quando **UNLIMITED** for especificado, o arquivo aumentará até que o disco esteja cheio. Especificar um valor inferior a 2 MB gera o erro MSG_MAXSIZE_TOO_SMALL. O valor padrão é **UNLIMITED**.  
  
 MAX_ROLLOVER_FILES **=** _integer_ | **UNLIMITED**  
 Especifica o número máximo de arquivos a serem retidos no sistema de arquivos. Ao configurar MAX_ROLLOVER_FILES=0 não haverá nenhum limite ao número de arquivos de substituição a serem criados. O valor padrão é 0. O número máximo de arquivos que pode ser especificado é 2.147.483.647.  
  
 MAX_FILES =*integer*  
 Especifica o número máximo de arquivos de auditoria que pode ser criado. Não substitui o primeiro arquivo quando o limite é atingido. Quando o limite de MAX_FILES é atingido, qualquer ação que provoque eventos de auditoria adicionais falhará com um erro.  
**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior.  
  
 RESERVE_DISK_SPACE **=** { ON | OFF }  
 Essa opção pré-aloca o arquivo no disco para o valor MAXSIZE. Só será aplicável se MAXSIZE não for igual a UNLIMITED. O valor padrão é OFF.  
  
 QUEUE_DELAY **=** _integer_  
 Determina a hora, em milissegundos, que pode decorrer antes que o processamento das ações de auditoria seja forçado. Um valor 0 indica entrega síncrona. O valor mínimo de atraso de consulta configurável é 1000 (1 segundo), que é o padrão. O máximo é 2.147.483.647 (2.147.483.647 segundos ou 24 dias, 20 horas, 31 minutos, 23.647 segundos). A especificação de um número inválido gera o erro MSG_INVALID_QUEUE_DELAY.  
  
 ON_FAILURE **=** { CONTINUE | SHUTDOWN | FAIL_OPERATION}  
 Indica se a instância que grava no destino deverá falhar, continuar ou parar se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não puder gravar no log de auditoria.  
  
 CONTINUE  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] As operações continuam. Os registros de auditoria não são retidos. A auditoria continua tentando registrar eventos em log e retoma se a condição de falha é resolvida. A seleção da opção Continuar pode permitir atividades não auditadas, o que pode violar as políticas de segurança. Use essa opção, quando continuar a operação do [!INCLUDE[ssDE](../../includes/ssde-md.md)] é mais importante do que manter uma auditoria completa.  
  
SHUTDOWN  
Força a instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a ser desligada, caso o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não possa gravar dados no destino de auditoria por qualquer motivo. O logon que executa a instrução `ALTER` deve ter a permissão `SHUTDOWN` no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O comportamento de desligamento persiste mesmo se a permissão `SHUTDOWN` é revogada posteriormente do logon em execução. Se o usuário não tiver essa permissão, a instrução falhará e a auditoria não será modificada. Use a opção quando uma falha de auditoria puder comprometer a segurança ou a integridade do sistema. Para obter mais informações, consulte [SHUTDOWN](../../t-sql/language-elements/shutdown-transact-sql.md). 
  
 FAIL_OPERATION  
 Haverá falha nas ações do banco de dados se elas provocarem eventos auditados. As ações que não causam eventos auditados podem continuar, mas nenhum evento auditado pode ocorrer. A auditoria continua tentando registrar eventos em log e retoma se a condição de falha é resolvida. Use essa opção, quando manter uma auditoria completa for mais importante do que o acesso total ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
 **Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior.   
  
 STATE **=** { ON | OFF }  
 Permite ou não que a auditoria colete registros. A alteração do estado de uma auditoria em execução (de ON para OFF) cria uma entrada de auditoria indicando que a auditoria foi interrompida, a entidade que interrompeu a auditoria e a hora da interrupção.  
  
 MODIFY NAME = *new_audit_name*  
 Altera o nome da auditoria. Não pode ser usado com nenhuma outra opção.  
  
 predicate_expression  
 Especifica a expressão de predicado usada para determinar se um evento deve ser processado ou não. As expressões de predicado são limitadas a 3.000 caracteres, o que limita os argumentos de cadeia de caracteres.  
 **Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior.  
  
 event_field_name  
 É o nome do campo de evento que identifica a origem do predicado. Campos de auditoria são descritos em [sys.fn_get_audit_file &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md). Todos os campos podem ser auditados menos `file_name` e `audit_file_offset`.  
 **Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior.  
  
 número  
 É qualquer tipo numérico, incluindo **decimal**. Limitações são a falta de memória física disponível ou um número que é muito grande para ser representado como um inteiro de 64 bits.  
 **Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior.  
  
 ' string '  
 Uma cadeia de caracteres ANSI ou Unicode, conforme requerido pela comparação de predicado. Nenhuma conversão de tipo de cadeia de caracteres implícita é executada para as funções de comparação de predicado. A transferência do tipo incorreto resulta em um erro.  
 **Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior.  
  
## <a name="remarks"></a>Comentários  
 Você deve especificar pelo menos uma das cláusulas TO, WITH ou MODIFY NAME ao chamar ALTER AUDIT.  
  
 Você deve definir o estado de uma auditoria para a opção OFF para fazer alterações em uma auditoria. Se ALTER AUDIT for executada quando uma auditoria estiver habilitada com qualquer opção diferente de STATE=OFF, você receberá uma mensagem de erro MSG_NEED_AUDIT_DISABLED.  
  
 Você pode adicionar, alterar e remover especificações de auditoria sem parar uma auditoria.  
  
 Não é possível alterar o GUID de uma auditoria após a criação da auditoria.  
 
 A instrução **ALTER SERVER AUDIT** não pode ser usada dentro de uma transação de usuário.
 
## <a name="permissions"></a>Permissões  
 Para criar, alterar ou descartar uma entidade de auditoria de servidor, você deve ter a permissão ALTER ANY SERVER AUDIT ou CONTROL SERVER.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-changing-a-server-audit-name"></a>a. Alterando o nome de uma auditoria de servidor  
 O exemplo a seguir altera o nome da auditoria de servidor `HIPAA_Audit` para `HIPAA_Audit_Old`.  
  
```sql  
USE master  
GO  
ALTER SERVER AUDIT HIPAA_Audit  
WITH (STATE = OFF);  
GO  
ALTER SERVER AUDIT HIPAA_Audit  
MODIFY NAME = HIPAA_Audit_Old;  
GO  
ALTER SERVER AUDIT HIPAA_Audit_Old  
WITH (STATE = ON);  
GO  
```  
  
### <a name="b-changing-a-server-audit-target"></a>B. Alterando o destino de uma auditoria de servidor  
 O exemplo a seguir altera a auditoria de servidor denominada `HIPAA_Audit` para um destino de arquivo.  
  
```sql  
USE master  
GO  
ALTER SERVER AUDIT HIPAA_Audit  
WITH (STATE = OFF);  
GO  
ALTER SERVER AUDIT HIPAA_Audit  
TO FILE (FILEPATH ='\\SQLPROD_1\Audit\',  
          MAXSIZE = 1000 MB,  
          RESERVE_DISK_SPACE=OFF)  
WITH (QUEUE_DELAY = 1000,  
       ON_FAILURE = CONTINUE);  
GO  
ALTER SERVER AUDIT HIPAA_Audit  
WITH (STATE = ON);  
GO  
```  
  
### <a name="c-changing-a-server-audit-where-clause"></a>C. Alterando uma cláusula WHERE de auditoria de servidor  
 O exemplo a seguir modifica o cláusula where criada no exemplo C de [CREATE SERVER AUDIT &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-audit-transact-sql.md). A nova cláusula WHERE filtra o evento definido pelo usuário se de 27.  
  
```sql  
ALTER SERVER AUDIT [FilterForSensitiveData] WITH (STATE = OFF)  
GO  
ALTER SERVER AUDIT [FilterForSensitiveData]  
WHERE user_defined_event_id = 27;  
GO  
ALTER SERVER AUDIT [FilterForSensitiveData] WITH (STATE = ON);  
GO  
```  
  
### <a name="d-removing-a-where-clause"></a>D. Removendo uma cláusula WHERE  
 O exemplo a seguir remove uma expressão de predicado de cláusula WHERE.  
  
```sql  
ALTER SERVER AUDIT [FilterForSensitiveData] WITH (STATE = OFF)  
GO  
ALTER SERVER AUDIT [FilterForSensitiveData]  
REMOVE WHERE;  
GO  
ALTER SERVER AUDIT [FilterForSensitiveData] WITH (STATE = ON);  
GO  
```  
  
### <a name="e-renaming-a-server-audit"></a>E. Renomeando uma auditoria de servidor  
 O exemplo a seguir altera o nome da auditoria de servidor de `FilterForSensitiveData` para `AuditDataAccess`.  
  
```sql  
ALTER SERVER AUDIT [FilterForSensitiveData] WITH (STATE = OFF)  
GO  
ALTER SERVER AUDIT [FilterForSensitiveData]  
MODIFY NAME = AuditDataAccess;  
GO  
ALTER SERVER AUDIT [AuditDataAccess] WITH (STATE = ON);  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [DROP SERVER AUDIT &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-audit-transact-sql.md)   
 [CREATE SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-server-audit-specification-transact-sql.md)   
 [ALTER SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-audit-specification-transact-sql.md)   
 [DROP SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-server-audit-specification-transact-sql.md)   
 [CREATE DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-audit-specification-transact-sql.md)   
 [ALTER DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-audit-specification-transact-sql.md)   
 [DROP DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-audit-specification-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [sys.fn_get_audit_file &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md)   
 [sys.server_audits &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audits-transact-sql.md)   
 [sys.server_file_audits &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-file-audits-transact-sql.md)   
 [sys.server_audit_specifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql.md)   
 [sys.server_audit_specification_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql.md)   
 [sys.database_audit_specifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql.md)   
 [sys.database_audit_specification_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql.md)   
 [sys.dm_server_audit_status &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql.md)   
 [sys.dm_audit_actions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql.md)   
 [Criar uma auditoria de servidor e uma especificação de auditoria de servidor](../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
  
