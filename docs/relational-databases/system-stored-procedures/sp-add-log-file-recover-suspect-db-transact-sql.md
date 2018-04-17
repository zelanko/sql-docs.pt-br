---
title: sp_add_log_file_recover_suspect_db (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_add_log_file_recover_suspect_db_TSQL
- sp_add_log_file_recover_suspect_db
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_log_file_recover_suspect_db
ms.assetid: b41ca3a5-7222-4c22-a012-e66a577a82f6
caps.latest.revision: 37
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1623d485132881e7d4df61926dc425257e3113b3
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/10/2018
---
# <a name="spaddlogfilerecoversuspectdb-transact-sql"></a>sp_add_log_file_recover_suspect_db (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Adiciona um arquivo de log a um grupo de arquivos quando a recuperação não pode ser concluída em um banco de dados devido a espaço insuficiente de log (erro 9002). Depois que o arquivo é adicionado, **sp_add_log_file_recover_suspect_db** desativa a configuração suspeita e conclui a recuperação do banco de dados. Os parâmetros são os mesmos de ALTER DATABASE *database_name* ADD LOG FILE.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_add_log_file_recover_suspect_db [ @dbName= ] 'database' ,   
    [ @name = ] 'logical_file_name' ,   
    [ @filename= ] 'os_file_name' ,   
    [ @size = ] 'size' ,   
    [ @maxsize = ] 'max_size' ,   
    [ @filegrowth = ] 'growth_increment'  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@dbName =** ] **'***banco de dados***'**  
 É o nome do banco de dados. *banco de dados* é **sysname**, sem padrão.  
  
 [ **@name=** ] **'***logical_file_name***'**  
 É o nome usado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] quando um arquivo é referenciado. O nome deve ser exclusivo no servidor. *logical_file_name* é **nvarchar (260)**, sem padrão.  
  
 [ **@filename =** ] **'***os_file_name***'**  
 É o caminho e o nome de arquivo usados pelo sistema operacional para o arquivo. O arquivo deve residir no servidor no qual o [!INCLUDE[ssDE](../../includes/ssde-md.md)] está instalado. *os_file_name* é **nvarchar (260)**, sem padrão.  
  
 [ **@size=** ] **'***size* **'**  
 É o tamanho inicial do arquivo. *tamanho* é **nvarchar (20)**, com um padrão NULL. Especifique um número inteiro; não inclua um decimal. Os sufixos MB e KB podem ser usados para especificar megabytes ou quilobytes. O padrão é MB. O valor mínimo é 512 KB. Se *tamanho* não for especificado, o padrão é 1 MB.  
  
 [ **@maxsize=** ] **'***max_size* **'**  
 É o tamanho máximo para o qual o arquivo pode crescer. *max_size* é **nvarchar (20)**, com um padrão NULL. Especifique um número inteiro; não inclua um decimal. Os sufixos MB e KB podem ser usados para especificar megabytes ou quilobytes. O padrão é MB.  
  
 Se *max_size* não for especificado, o arquivo crescerá até que o disco está cheio. O log de aplicativo do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows adverte o administrador quando o disco está quase cheio.  
  
 [ **@filegrowth=** ] **'***growth_increment* **'**  
 É a quantidade de espaço adicionada ao arquivo a cada vez que novo espaço é necessário. *growth_increment* é **nvarchar (20)**, com um padrão NULL. Um valor de 0 indica que não houve crescimento. Especifique um número inteiro; não inclua um decimal. O valor pode ser especificado em MB, KB ou porcentagem (%). Quando a % é especificada, o incremento de crescimento é a porcentagem especificada do tamanho do arquivo no momento em que ocorre o incremento. Se um número for especificado sem um sufixo MB, KB, ou %, o padrão será MB.  
  
 Se *growth_increment* for NULL, o valor padrão é 10% e o valor de tamanho mínimo é 64 KB. O tamanho especificado é arredondado para o mais próximo de 64 KB.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhuma  
  
## <a name="permissions"></a>Permissões  
 Execute permissões padrão para membros de **sysadmin** função de servidor fixa. Essas permissões não são transferíveis.  
  
## <a name="examples"></a>Exemplos  
 No exemplo a seguir, o banco de dados `db1` foi marcado como suspeito durante a recuperação, devido a espaço insuficiente de log (erro 9002).  
  
```  
USE master;  
GO  
EXEC sp_add_log_file_recover_suspect_db db1, logfile2,  
'C:\Program Files\Microsoft SQL  
    Server\MSSQL13.MSSQLSERVER\MSSQL\Data\db1_logfile2.ldf',   
    '1MB';  
```  
  
## <a name="see-also"></a>Consulte também  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [sp_add_data_file_recover_suspect_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-data-file-recover-suspect-db-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
