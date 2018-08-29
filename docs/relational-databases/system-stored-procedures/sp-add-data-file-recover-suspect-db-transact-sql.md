---
title: sp_add_data_file_recover_suspect_db (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_add_data_file_recover_suspect_db
- sp_add_data_file_recover_suspect_db_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_data_file_recover_suspect_db
ms.assetid: b25262aa-a228-48b7-8739-6581c760b171
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d6d2facde85a46db3c54d3d94e7502e6341ae57a
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43021695"
---
# <a name="spadddatafilerecoversuspectdb-transact-sql"></a>sp_add_data_file_recover_suspect_db (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Adiciona um arquivo de dados a um grupo de arquivos quando a recuperação não consegue ser concluída em um banco de dados devido a espaço insuficiente no grupo de arquivos (erro 1105). Depois que o arquivo é adicionado, esse procedimento armazenado desativa a configuração suspeita e conclui a recuperação do banco de dados. Os parâmetros são os mesmos de ALTER DATABASE *database_name* ADD FILE.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_add_data_file_recover_suspect_db [ @dbName= ] 'database'   
    , [ @filegroup = ] 'filegroup_name'   
    , [ @name = ] 'logical_file_name'   
    , [ @filename= ] 'os_file_name'   
    , [ @size = ] 'size'   
    , [ @maxsize = ] 'max_size'   
    , [ @filegrowth = ] 'growth_increment'  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@dbName=** ] **' * * * banco de dados* **'**  
 É o nome do banco de dados. *banco de dados* está **sysname**, sem padrão.  
  
 [  **@filegroup=** ] **' * * * filegroup_name* **'**  
 É o grupo de arquivos ao qual adicionar o arquivo. *filegroup_name* está **nvarchar (260)**, com um padrão NULL, que indica que o arquivo primário.  
  
 [  **@name=** ] **' * * * logical_file_name* **'**  
 É o nome usado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para referenciar o arquivo. O nome deve ser exclusivo no servidor. *logical_file_name* está **nvarchar (260)**, sem padrão.  
  
 [  **@filename=** ] **' * * * os_file_name* **'**  
 É o caminho e o nome de arquivo usados pelo sistema operacional para o arquivo. O arquivo precisa residir em uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. *os_file_name* está **nvarchar (260)**, sem padrão.  
  
 [  **@size=** ] **' * * * tamanho* **'**  
 É o tamanho inicial do arquivo. *tamanho* está **nvarchar (20)**, com um padrão NULL. Especifique um número inteiro; não inclua um decimal. Os sufixos MB e KB podem ser usados para especificar megabytes ou quilobytes. O padrão é MB. O valor mínimo é 512 KB. Se *tamanho* não for especificado, o padrão é 1 MB.  
  
 [ **@maxsize=** ] **'***max_size* **'**  
 É o tamanho máximo para o qual o arquivo pode crescer. *max_size* está **nvarchar (20)**, com um padrão NULL. Especifique um número inteiro; não inclua um decimal. Os sufixos MB e KB podem ser usados para especificar megabytes ou quilobytes. O padrão é MB.  
  
 Se *max_size* não for especificado, o arquivo crescerá até que o disco está cheio. O log de aplicativo do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows adverte o administrador quando o disco está quase cheio.  
  
 [  **@filegrowth=** ] **' * * * growth_increment* **'**  
 É a quantidade de espaço adicionada ao arquivo a cada vez que novo espaço é necessário. *growth_increment* está **nvarchar (20)**, com um padrão NULL. Um valor de 0 indica que não houve crescimento. Especifique um número inteiro; não inclua um decimal. O valor pode ser especificado em MB, KB ou porcentagem (%). Quando a % é especificada, o incremento de crescimento é a porcentagem especificada do tamanho do arquivo no momento em que ocorre o incremento. Se um número for especificado sem um sufixo MB, KB, ou %, o padrão será MB.  
  
 Se *growth_increment* for NULL, o valor padrão é 10% e o valor mínimo é de 64 KB. O tamanho especificado é arredondado para o mais próximo de 64 KB.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="permissions"></a>Permissões  
 Execute permissões padrão para os membros de **sysadmin** função de servidor fixa. Essas permissões não são transferíveis.  
  
## <a name="examples"></a>Exemplos  
 No exemplo a seguir, o banco de dados `db1` foi marcado como suspeito durante a recuperação, devido a espaço insuficiente (erro 1105) no grupo de arquivos `fg1`.  
  
```  
USE master;  
GO  
EXEC sp_add_data_file_recover_suspect_db db1, fg1, file2,  
    'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data\db1_file2.mdf', '1MB';  
```  
  
## <a name="see-also"></a>Consulte também  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [sp_add_log_file_recover_suspect_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-log-file-recover-suspect-db-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
