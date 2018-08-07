---
title: CREATE SERVER AUDIT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/22/2018
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CREATE_SERVER_AUDIT_TSQL
- SERVER AUDIT
- SERVER_AUDIT_TSQL
- CREATE SERVER AUDIT
dev_langs:
- TSQL
helpviewer_keywords:
- server audit [SQL Server]
- CREATE SERVER AUDIT statement
- audits [SQL Server], creating
ms.assetid: 1c321680-562e-41f1-8eb1-e7fa5ae45cc5
caps.latest.revision: 44
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 7d16529308dc45fd64f6b16d7dec92f1fe8be8cc
ms.sourcegitcommit: e02c28b0b59531bb2e4f361d7f4950b21904fb74
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/02/2018
ms.locfileid: "39452110"
---
# <a name="create-server-audit-transact-sql"></a>CREATE SERVER AUDIT (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Cria um objeto de auditoria de servidor por meio do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Audit. Para obter mais informações, veja [Auditoria do SQL Server &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md).  

[!INCLUDE[ssMIlimitation](../../includes/sql-db-mi-limitation.md)]

 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
CREATE SERVER AUDIT audit_name  
{  
    TO { [ FILE (<file_options> [ , ...n ] ) ] | APPLICATION_LOG | SECURITY_LOG }  
    [ WITH ( <audit_options> [ , ...n ] ) ]   
    [ WHERE <predicate_expression> ]  
}  
[ ; ]  
  
<file_options>::=  
{  
        FILEPATH = 'os_file_path'  
    [ , MAXSIZE = { max_size { MB | GB | TB } | UNLIMITED } ]  
    [ , { MAX_ROLLOVER_FILES = { integer | UNLIMITED } } | { MAX_FILES = integer } ]  
    [ , RESERVE_DISK_SPACE = { ON | OFF } ]   
}  
  
<audit_options>::=  
{  
    [   QUEUE_DELAY = integer ]  
    [ , ON_FAILURE = { CONTINUE | SHUTDOWN | FAIL_OPERATION } ]  
    [ , AUDIT_GUID = uniqueidentifier ]  
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
  
## <a name="arguments"></a>Argumentos  
 TO { FILE | APPLICATION_LOG | SECURITY_LOG }  
 Determina o local do destino da auditoria. As opções são um arquivo binário, o log do Aplicativo do Windows ou o log de Segurança do Windows. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não poderá gravar no log de segurança do Windows se não forem definidas configurações adicionais no Windows. Para obter mais informações, veja [Gravar eventos de auditoria do SQL Server no log de segurança](../../relational-databases/security/auditing/write-sql-server-audit-events-to-the-security-log.md).  
  
 FILEPATH ='*os_file_path*'  
 O caminho do log de auditoria. O nome do arquivo é gerado com base no nome da auditoria e no GUID da auditoria.  
  
 MAXSIZE = { *max_size }*  
 Especifica o tamanho máximo até o qual o arquivo de auditoria pode crescer. O valor de *max_size* deve ser um inteiro seguido de MB, GB, TB ou UNLIMITED. O tamanho mínimo que você pode especificar para *max_size* é 2 MB e o máximo é 2.147.483.647 TB. Quando UNLIMITED é especificado, o arquivo aumenta até que o disco esteja completo. (0 também indica UNLIMITED.) A especificação de um valor inferior a 2 MB gera o erro MSG_MAXSIZE_TOO_SMALL. O valor padrão é UNLIMITED.  
  
 MAX_ROLLOVER_FILES =*{ integer* | UNLIMITED }  
 Especifica o número máximo de arquivos a serem retidos no sistema de arquivos além do arquivo atual. O valor *MAX_ROLLOVER_FILES* deve ser um inteiro ou UNLIMITED. O valor padrão é UNLIMITED. Este parâmetro é avaliado sempre que a auditoria é reiniciada (o que pode ocorrer quando a instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] é reiniciada ou quando a auditoria é desativada e, em seguida, reativada) ou quando um novo arquivo é necessário porque o valor máximo de MAXSIZE foi alcançado. Quando *MAX_ROLLOVER_FILES* é avaliado, se o número de arquivos excede a configuração de *MAX_ROLLOVER_FILES*, o arquivo mais antigo é excluído. Como resultado, quando a configuração de *MAX_ROLLOVER_FILES* é 0, um novo arquivo é criado sempre que a configuração de *MAX_ROLLOVER_FILES* é avaliada. Somente um arquivo é excluído automaticamente quando a configuração de *MAX_ROLLOVER_FILES* é avaliada. Portanto, quando o valor de *MAX_ROLLOVER_FILES* é reduzido, o número de arquivos não diminui, a menos que os arquivos antigos sejam excluídos manualmente. O número máximo de arquivos que pode ser especificado é 2.147.483.647.  
  
 MAX_FILES =*integer*  
 **Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica o número máximo de arquivos de auditoria que pode ser criado. Não substitui o primeiro arquivo quando o limite é atingido. Quando o limite de MAX_FILES é atingido, qualquer ação que causa a geração de eventos adicionais falha com um erro.  
  
 RESERVE_DISK_SPACE = { ON | OFF }  
 Essa opção pré-aloca o arquivo no disco para o valor MAXSIZE. Isso só valerá se MAXSIZE não for igual a UNLIMITED. O valor padrão é OFF.  
  
 QUEUE_DELAY =*integer*  
 Determina a hora, em milissegundos, que pode decorrer antes que o processamento das ações de auditoria seja forçado. Um valor 0 indica entrega síncrona. O valor mínimo de atraso de consulta configurável é 1000 (1 segundo), que é o padrão. O máximo é 2.147.483.647 (2.147.483.647 segundos ou 24 dias, 20 horas, 31 minutos, 23.647 segundos). A especificação de um número inválido, gera o erro MSG_INVALID_QUEUE_DELAY.  
  
 ON_FAILURE = { CONTINUE | SHUTDOWN | FAIL_OPERATION }  
 Indica se a instância que grava no destino deverá falhar, continuar ou parar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se o destino não puder gravar no log de auditoria. O valor padrão é CONTINUE.  
  
 CONTINUE  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] As operações continuam. Os registros de auditoria não são retidos. A auditoria continua tentando registrar eventos em log e retoma se a condição de falha é resolvida. A seleção da opção Continuar pode permitir atividades não auditadas, o que pode violar as políticas de segurança. Use essa opção, quando continuar a operação do [!INCLUDE[ssDE](../../includes/ssde-md.md)] é mais importante do que manter uma auditoria completa.  
  
SHUTDOWN  
Força a instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a ser desligada, caso o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não possa gravar dados no destino de auditoria por qualquer motivo. O logon que executa a instrução `CREATE SERVER AUDIT` deve ter a permissão `SHUTDOWN` no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O comportamento de desligamento persiste mesmo se a permissão `SHUTDOWN` é revogada posteriormente do logon em execução. Se o usuário não tiver essa permissão, a instrução falhará e a auditoria não será criada. Use a opção quando uma falha de auditoria puder comprometer a segurança ou a integridade do sistema. Para obter mais informações, consulte [SHUTDOWN](../../t-sql/language-elements/shutdown-transact-sql.md).  
  
 FAIL_OPERATION  
 Haverá falha nas ações do banco de dados se elas provocarem eventos auditados. As ações que não causam eventos auditados podem continuar, mas nenhum evento auditado pode ocorrer. A auditoria continua tentando registrar eventos em log e retoma se a condição de falha é resolvida. Use essa opção, quando manter uma auditoria completa for mais importante do que o acesso total ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
**Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].

 AUDIT_GUID =*uniqueidentifier*  
 Para dar suporte a cenários, como espelhamento de banco de dados, uma auditoria precisa de um GUID específico que corresponda ao GUID encontrado no banco de dados espelhado. O GUID não pode ser modificado depois que a auditoria foi criada.  
  
 predicate_expression  
 **Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Especifica a expressão de predicado usada para determinar se um evento deve ser processado ou não. As expressões de predicado são limitadas a 3.000 caracteres, o que limita os argumentos de cadeia de caracteres.  
  
 event_field_name  
 **Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 É o nome do campo de evento que identifica a origem do predicado. Campos de auditoria são descritos em [sys.fn_get_audit_file &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md). Todos os campos podem ser filtrados, exceto `file_name`, `audit_file_offset` e `event_time`.  

> [!NOTE]  
>  Embora os campos `action_id` e `class_type` sejam do tipo **varchar** em sys.fn_get_audit_file, eles podem ser usados somente com números quando são uma origem de predicado para a filtragem. Para obter a lista de valores a serem usados com `class_type`, execute a seguinte consulta:  
> ```sql
> SELECT spt.[name], spt.[number]
> FROM   [master].[dbo].[spt_values] spt
> WHERE  spt.[type] = N'EOD'
> ORDER BY spt.[name];
> ```


 number  
 **Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 É qualquer tipo numérico, incluindo **decimal**. Limitações são a falta de memória física disponível ou um número que é muito grande para ser representado como um inteiro de 64 bits.  
  
 ' string '  
 **Aplica-se a**: do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ao [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Uma cadeia de caracteres ANSI ou Unicode, conforme requerido pela comparação de predicado. Nenhuma conversão de tipo de cadeia de caracteres implícita é executada para as funções de comparação de predicado. A transferência do tipo incorreto resulta em um erro.  
  
## <a name="remarks"></a>Remarks  
 Quando uma auditoria de servidor é criada, ela permanece em um estado desabilitado.  
  
 A instrução CREATE SERVER AUDIT está no escopo de uma transação. Se a transação for revertida, a instrução também será revertida.  
  
## <a name="permissions"></a>Permissões  
 Para criar, alterar ou descartar uma auditoria de servidor, as entidades devem ter a permissão ALTER ANY SERVER AUDIT ou CONTROL SERVER.  
  
 Quando você está salvando informações de auditoria em um arquivo, para ajudar a impedir falsificação, você pode restringir o acesso ao local do arquivo.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-creating-a-server-audit-with-a-file-target"></a>A. Criando uma auditoria de servidor com um arquivo de destino  
 O exemplo a seguir cria uma auditoria de servidor denominada `HIPPA_Audit` com um arquivo binário como o destino e nenhuma opção.  
  
```sql  
CREATE SERVER AUDIT HIPAA_Audit  
    TO FILE ( FILEPATH ='\\SQLPROD_1\Audit\' );  
```  
  
### <a name="b-creating-a-server-audit-with-a-windows-application-log-target-with-options"></a>B. Criando uma auditoria de servidor com um destino de log de aplicativos do Windows com opções  
 O exemplo a seguir cria uma auditoria de servidor denominada `HIPPA_Audit` com o conjunto de destino para o log de aplicativos do Windows. A fila é gravada a cada segundo e o mecanismo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é desligado em caso de falha.  
  
```sql  
CREATE SERVER AUDIT HIPAA_Audit  
    TO APPLICATION_LOG  
    WITH ( QUEUE_DELAY = 1000,  ON_FAILURE = SHUTDOWN);  
```  
  
###  <a name="ExampleWhere"></a> C. Criando uma auditoria de servidor que contém uma cláusula WHERE  
 O exemplo a seguir cria um banco de dados, um esquema e duas tabelas para o exemplo. A tabela chamada `DataSchema.SensitiveData` contém dados confidenciais e o acesso à tabela deve ser registrado na auditoria. A tabela denominada `DataSchema.GeneralData` não contém dados confidenciais. A especificação de auditoria de banco de dados audita acesso a todos os objetos no esquema `DataSchema`. A auditoria de servidor é criada com uma cláusula WHERE que limita a auditoria de servidor apenas à tabela `SensitiveData`. A auditoria de servidor supõe que exista uma pasta de auditoria em `C:\SQLAudit`.  
  
```sql  
CREATE DATABASE TestDB;  
GO  
USE TestDB;  
GO  
CREATE SCHEMA DataSchema;  
GO  
CREATE TABLE DataSchema.GeneralData (ID int PRIMARY KEY, DataField varchar(50) NOT NULL);  
GO  
CREATE TABLE DataSchema.SensitiveData (ID int PRIMARY KEY, DataField varchar(50) NOT NULL);  
GO  
-- Create the server audit in the master database  
USE master;  
GO  
CREATE SERVER AUDIT AuditDataAccess  
    TO FILE ( FILEPATH ='C:\SQLAudit\' )  
    WHERE object_name = 'SensitiveData' ;  
GO  
ALTER SERVER AUDIT AuditDataAccess WITH (STATE = ON);  
GO  
-- Create the database audit specification in the TestDB database  
USE TestDB;  
GO  
CREATE DATABASE AUDIT SPECIFICATION [FilterForSensitiveData]  
FOR SERVER AUDIT [AuditDataAccess]   
ADD (SELECT ON SCHEMA::[DataSchema] BY [public])  
WITH (STATE = ON);  
GO  
-- Trigger the audit event by selecting from tables  
SELECT ID, DataField FROM DataSchema.GeneralData;  
SELECT ID, DataField FROM DataSchema.SensitiveData;  
GO  
-- Check the audit for the filtered content  
SELECT * FROM fn_get_audit_file('C:\SQLAudit\AuditDataAccess_*.sqlaudit',default,default);  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER SERVER AUDIT &#40;Transact-SQL&#41;](../../t-sql/statements/alter-server-audit-transact-sql.md)   
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
 [sys.dm_audit_class_type_map &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql.md)   
 [Criar uma auditoria de servidor e uma especificação de auditoria de servidor](../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
  
