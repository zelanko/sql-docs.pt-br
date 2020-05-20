---
title: managed_backup. sp_backup_on_demand (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- smart_admin.sp_backup_on_demand
- smart_admin.sp_backup_on_demand_TSQL
- sp_backup_on_demand_TSQL
- sp_backup_on_demand
dev_langs:
- TSQL
helpviewer_keywords:
- smart_admin.sp_backup_on_demand
- sp_backup_on_demand
ms.assetid: 638f809f-27fa-4c44-a549-9cf37ecc920c
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: bb2bda2d58504033469e8ed0f6455784efb113b8
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82830417"
---
# <a name="managed_backupsp_backup_on_demand-transact-sql"></a>managed_backup. sp_backup_on_demand (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Solicita que o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] execute um backup do banco de dados especificado.  
  
 Use esse procedimento armazenado para executar backups ad hoc para um banco de dados configurado com o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]. Isso impede que qualquer interrupção na cadeia de backup e [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] processos esteja ciente e o backup seja armazenado no mesmo contêiner de armazenamento de BLOBs do Azure.  
  
 Após a conclusão bem-sucedida do backup, o caminho do arquivo de backup completo será retornado. Isso inclui o nome e o local do novo arquivo de backup decorrente da operação de backup.  
  
 Um erro será retornado se o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] estiver no processo de executar um backup do tipo especificado para o banco de dados especificado. Nesse caso, a mensagem de erro retornada inclui o caminho de arquivo do backup completo em que o backup atual está sendo carregado.  
   
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
EXEC managed_backup.sp_backup_on_demand   
[@database_name  =]  'database name',[@type = ] { 'Database' | 'Log' }  
  
```  
  
##  <a name="arguments"></a><a name="Arguments"></a>Argumentos  
 @database_name  
 O nome do banco de dados em que o backup será executado. O @database_name é **sysname**.  
  
 @type  
 O tipo de backup a ser executado: Banco de Dados ou Log. O @type parâmetro é **nvarchar (32)**.  
  
## <a name="return-code-value"></a>Valor do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 Exige associação à função de banco de dados **db_backupoperator** , com permissões **ALTER ANY CREDENTIAL** e as permissões **EXECUTE** no procedimento armazenado **sp_delete_backuphistory**.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir faz uma solicitação de backup de banco de dados para o banco de dados ' TestDB '. Esse banco de dados tem [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] habilitado.  
  
```  
Use MSDB  
Go  
EXEC managed_backup.sp_backup_on_demand  
 @database_name = 'TestDB'  
,@type = 'Database'  
  
```  
  
 Para cada snippet de código, selecione 'tsql' no campo do atributo de idioma.  
  
  
