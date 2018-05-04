---
title: managed_backup.sp_backup_on_demand (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
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
caps.latest.revision: 13
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: cb3620bc20ae46dd2aac4fa89d4031ab996ed0b1
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="managedbackupspbackupondemand-transact-sql"></a>managed_backup.sp_backup_on_demand (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Solicita que o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] execute um backup do banco de dados especificado.  
  
 Use esse procedimento armazenado para executar backups ad hoc para um banco de dados configurado com o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]. Isso evita qualquer interrupção na cadeia de backup e os processos do [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] estão cientes e o backup é armazenado no mesmo contêiner de armazenamento de Blob do Windows Azure.  
  
 Após a conclusão bem-sucedida do backup, o caminho do arquivo de backup completo será retornado. Isso inclui o nome e o local do novo arquivo de backup decorrente da operação de backup.  
  
 Um erro será retornado se o [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] estiver no processo de executar um backup do tipo especificado para o banco de dados especificado. Nesse caso, a mensagem de erro retornada inclui o caminho de arquivo do backup completo em que o backup atual está sendo carregado.  
   
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
EXEC managed_backup.sp_backup_on_demand   
[@database_name  =]  'database name',[@type = ] { 'Database' | 'Log' }  
  
```  
  
##  <a name="Arguments"></a> Argumentos  
 @database_name  
 O nome do banco de dados em que o backup será executado. O @database_name é **SYSNAME**.  
  
 @type  
 O tipo de backup a ser executado: Banco de Dados ou Log. O @type parâmetro é **nvarchar (32)**.  
  
## <a name="return-code-value"></a>Valor do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 Exige associação à função de banco de dados **db_backupoperator** , com permissões **ALTER ANY CREDENTIAL** e as permissões **EXECUTE** no procedimento armazenado **sp_delete_backuphistory**.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir faz uma solicitação de backup de banco de dados para o banco de dados ‘TestDB’. Esse banco de dados tem [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] habilitado.  
  
```  
Use MSDB  
Go  
EXEC managed_backup.sp_backup_on_demand  
 @database_name = 'TestDB'  
,@type = 'Database'  
  
```  
  
 Para cada trecho de código, selecione 'tsql' no campo do atributo de idioma.  
  
  
